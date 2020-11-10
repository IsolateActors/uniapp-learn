<template>
	<view class="goods-list">
		<view class="goods-item" v-for="(item,index) in goods" :key="index">
			<image :src="item.goods_big_logo" mode=""></image>
			<view class="price">
				<text>￥{{item.goods_price}}</text>
				<text>￥{{item.goods_price + 1000}}</text>
			</view>
			<text class="name">
				{{item.goods_name}}
			</text>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				
			}
		},
		props:['goods']
	}
</script>

<style lang="scss">
	.goods-list{
		padding: 0 15rpx;
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		
		.goods-item{
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
</style>
