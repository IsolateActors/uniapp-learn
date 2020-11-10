<template>
	<view class="contact">
		<image class="img" src="https://img95.699pic.com/photo/50058/9486.jpg_wh300.jpg" mode=""></image>
		<view class="info">
			<view @click="callPhone">联系电话：{{phoneNum}}(点击拨打)</view>
			<view class="">地址：广东省广州市海珠区广州塔</view>
		</view>
		<map class="map" :latitude="latitude" :longitude="longitude" :markers="markers"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				phoneNum: "12345678900",
				longitude: 113.331084,
				latitude: 23.112223,
				scale: 13,
				markers:[
					{
						longitude: 113.331084,
						latitude: 23.112223,
						iconPath: '../../static/logo.png',
						width: 20,
						height: 20
					},
				]
			}
		},
		methods: {
			callPhone(){
				uni.makePhoneCall({
					phoneNumber: this.phoneNum
				})
			}
		}
	}
</script>

<style lang="scss">
	.contact{
		.img{
			width: 750rpx;
			height: 320rpx;
		}
		
		.info{
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view{
				line-height: 80rpx;
				border-bottom: 1px solid #eee;
			}
		}
		
		.map{
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
