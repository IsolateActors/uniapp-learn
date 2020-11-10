<template>
	<view class="goods-list">
		<goods-list :goods="goods"></goods-list>
		<view class="isOver" v-if="flag">----------已经没有数据----------</view>
	</view>
</template>

<script>
	// import goodsList from '@/components/goods-list/goods-list.vue'
	export default {
		data() {
			return {
				pagenum: 1,
				pagesize: 10,
				goods: [],
				flag: false
			}
		},
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom() {
			console.log("触底了")
			this.pagenum++;
			this.getGoodsList();
		},
		onPullDownRefresh() {
			console.log("下拉刷新")
			this.pagenum = 1;
			this.goods = [];
			this.flag = false;
			setTimeout(()=>{
				this.getGoodsList(()=>{
					uni.stopPullDownRefresh();
				});
			},1000)
			
		},
		methods: {
			async getGoodsList(callback){
				const res = await this.$myRequest({
					url: "/goods/search?pagenum=" + this.pagenum + "&pagesize=" + this.pagesize
				})
				console.log(res)
				if(Math.ceil(res.data.message.total/this.pagesize) <= res.data.message.pagenum ){
					this.flag = true
				}
				this.goods = [...this.goods, ...res.data.message.goods]
				callback && callback()
			}
		},
		// components:{
		// 	'goods-list': goodsList
		// }
	}
</script>

<style lang="scss">
	.goods-list{
		background-color: #eee;
	}
	.isOver{
		width: 100vw;
		height: 50px;
		line-height: 50px;
		text-align: center;
		font-size: 28rpx;
	}
</style>
