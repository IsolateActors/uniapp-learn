<template>
	<view class="home">
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" circular>
			<swiper-item v-for="(item,index) in swipers" :key="index">
				<view class="swiper-item"><image :src="item.image_src" mode=""></image></view>
			</swiper-item>
		</swiper>
		
		<!-- 导航区域 -->
		<!-- <view class="nav">
			<view class="nav-item" v-for="(item, index) in catitems" :key="index" @click="navItemClick(item)">
				<image :src="item.image_src" mode=""></image>
			</view>
		</view> -->
		
		<view class="nav">
			<view class="nav-item" v-for="(item, index) in navs" :key="index" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		
		<!-- 楼层商品区 -->
		<view class="floor-data" v-for="(item, index) in floordatas" :key="index">
			<view class="title">{{item.floor_title.name}}</view>
			<view class="product-list">
				<view class="product-item" v-for="(itemChild,indexChild) in item.product_list" :key="indexChild">
					<image :src="itemChild.image_src" mode=""></image>
					<!-- <view class="price">
						<text>￥2199</text>
						<text>￥2499</text>
					</view> -->
					<text class="name">
						{{itemChild.name}}
					</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	
	export default {
		data() {
			return {
				swipers: [],
				floordatas: [],
				// catitems:[]
				navs: [
					{
						icon: "iconfont icon-ziyuan",
						title: "超市",
						path: "/pages/goods/goods"
					},
					{
						icon: "iconfont icon-guanyuwomen",
						title: "关于我们",
						path: "/pages/contact/contact"
					},
					{
						icon: "iconfont icon-tupian",
						title: "商品分类",
						path: "/pages/categories/categories"
					},
					{
						icon: "iconfont icon-shipin",
						title: "视频",
						path: "/pages/videos/videos"
					}
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getFloorDatas()
			// this.getCatitems()
		},
		methods: {
			// 获取轮播图
			async getSwipers(){
				console.log("获取轮播图")
				// uni.request({
				// 	url:"https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata",
				// 	method:"GET",
				// 	success: (res) => {
				// 		console.log(res.data)
				// 		if(res.data.meta.status !== 200){
				// 			return uni.showToast({
				// 				title:"数据获取失败"
				// 			})
				// 		}
				// 		this.swipers = res.data.message
				// 	}
				// })
				
				const res = await this.$myRequest({
					url: "/home/swiperdata",
				})
				console.log(res)
				this.swipers = res.data.message
			},
			
			// 获取导航菜单
			// async getCatitems(){
			// 	const res = await this.$myRequest({
			// 		url:"/home/catitems"
			// 	})
			// 	console.log(res)
			// 	this.catitems = res.data.message
			// },
			
			// 获取楼层商品列表数据
			async getFloorDatas(){
				const res = await this.$myRequest({
					url:"/home/floordata"
				})
				console.log(res)
				this.floordatas = res.data.message
			},
			
			// 导航
			// navItemClick(item){
			// 	console.log(item)
			// 	if(item.navigator_url !== undefined){
			// 		if(item.open_type == "switchTab"){
			// 			console.log(item.navigator_url)
			// 			uni.navigateTo({
			// 				url:item.navigator_url
			// 			})
			// 		}
			// 	}
			// }
			
			// 导航
			navItemClick(url){
				console.log(url)
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			
			.swiper-item{
				width: 100%;
				height: 100%;
			}
			
			image{
				width: 100%;
				height: 100%;
			}
		}
		
		// .nav{
		// 	display: flex;
			
		// 	.nav-item{
		// 		// width: 25%;
		// 		flex: 1;
		// 		text-align: center;
		// 		padding: 20rpx;
		// 		box-sizing: border-box;
		// 	}
		// 	image{
		// 		width: 100%;
		// 		height: 150rpx;
		// 	}
		// }
		
		.nav{
			display: flex;
			
			.nav-item{
				// width: 25%;
				flex: 1;
				text-align: center;
				
				view{
					width: 120rpx;
					height: 120rpx;
					background-color: $shop-color;
					border-radius: 60rpx;
					margin: 10rpx auto;
					line-height: 120rpx;
					color: #fff;
					font-size: 50rpx;
				}
				
				text{
					font-size: 30rpx;
				}
			}
			
			.icon-tupian{
				font-size: 45rpx;
			}
			
		}
		
		
		
		.floor-data{
			background-color: #eee;
			overflow: hidden;
			// margin-top: 20rpx;
			
			.title{
				height: 100rpx;
				line-height: 100rpx;
				color: $shop-color;
				text-align: center;
				letter-spacing: 40rpx;
				background-color: #fff;
				margin: 7rpx 0;
			}
			
			.product-list{
				padding: 0 15rpx;
				display: flex;
				flex-wrap: wrap;
				justify-content: space-between;
				
				.product-item{
					background-color: #fff;
					width: 355rpx;
					margin: 10rpx 0;
					padding: 15rpx;
					box-sizing: border-box;
				}
				image{
					width: 100%;
					height: 300rpx;
					display: block;
					margin: 0 auto;
				}
				
				.price{
					color: $shop-color;
					font-size: 36rpx;
					text:nth-child(2){
						color: #ccc;
						font-size: 28rpx;
						margin-left: 17rpx;
						text-decoration: line-through;
					}
				}
				
				.name{
					font-size: 28rpx;
					line-height: 50rpx;
					padding-bottom: 10rpx;
					padding-top: 10rpx;
					overflow : hidden;
					text-overflow: ellipsis;
					display: -webkit-box;
					-webkit-line-clamp: 2;
					-webkit-box-orient: vertical;
				}
			}
		}
	}
</style>
