<template>
	<view class="categories">
		<scroll-view scroll-y class="left">
			<view 
			@click="leftChildHandle(index)"
			:class="active===index?'active':''" 
			v-for="(item, index) in categories" 
			:key="item.cat_id">{{item.cat_name}}</view>
		</scroll-view>
		
		<scroll-view scroll-y class="right" enable-flex="true">
			<view class="bigbox" v-for="(item,index) in rightChildList" :key="item.cat_id">
				<view class="title">
					-- {{item.cat_name}} --
				</view>
				<view class="content">
					<view class="box" v-for="(itemchild, indexchild) in item.children" :key="item.cat_id">
						<image :src="itemchild.cat_icon" mode=""></image>
						<text>{{itemchild.cat_name}}</text>
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				categories: [],
				rightChildList: [],
				active: 0
			}
		},
		onLoad() {
			this.getCategories()
		},
		methods: {
			async getCategories(){
				const res = await this.$myRequest({
					url: "/categories"
				})
				console.log(res)
				this.categories = res.data.message
				this.rightChildList = this.categories[0].children
			},
			leftChildHandle(index){
				console.log(index)
				this.active = index
				this.rightChildList = this.categories[index].children
			}
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.categories{
		height: 100%;
		display: flex;
		
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 1px solid #eee;
			}
			.active{
				background-color: $shop-color;
				color: #fff;
			}
		}
		
		.right{
			width: 500rpx;
			display: flex;
			flex-direction: column;
			padding: 20rpx;
			
			.bigbox{
				margin: 0 auto;
				width: 100%;
			}
			
			.title{
				height: 60rpx;
				line-height: 60rpx;
				text-align: center;
				font-size: 30rpx;
				color: #ccc;
				
			}
			.content{
				display: flex;
				flex-wrap: wrap;
				padding: 10rpx;
				width: 100%;
			}
			.box{
				display: flex;
				flex-direction: column;
				box-sizing: border-box;
				padding: 10rpx;
				width: 33%;
			}
			
			image{
				width: 100rpx;
				height: 100rpx;
				margin: auto;
			}
			text{
				height: 50rpx;
				line-height: 50rpx;
				font-size: 26rpx;
				text-align: center;
				color: #ccc;
			}
		}
	}
</style>
