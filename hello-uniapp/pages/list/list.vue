<template>
	<view>
		<view class="">
			这是列表
		</view>
		<view v-for='item in list' class="box-item">
			{{item}}
		</view>
		<button @click="pullDown">下拉刷新</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:['前端', 'Ja', "UI", "测试", '前端', 'Ja', "UI", "测试"]
			}
		},
		methods: {
			pullDown(){
				uni.startPullDownRefresh()
			}
		},
		onReachBottom(){
			console.log("页面触地")
			this.list = [...this.list, ...['前端', "UI", "测试", 'Ja']]
		},
		onPullDownRefresh(){
			console.log("触发下拉刷新")
			setTimeout(()=>{
				this.list = ['前端', "UI", "测试", 'Ja']
				uni.stopPullDownRefresh()
			}, 2000)
		}
	}
</script>

<style>
.box-item {
	height: 100px;
	line-height: 100px;
}
</style>
