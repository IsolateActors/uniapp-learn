<template>
	<view class="">
		首页
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swipers: []
			}
		},
		onLoad() {
			this.getSwipers()
		},
		methods: {
			// 获取轮播图
			getSwipers(){
				console.log("获取轮播图")
				uni.request({
					url:"https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata",
					method:"GET",
					success: (res) => {
						console.log(res.data)
						if(res.data.meta.status !== 200){
							return uni.showToast({
								title:"数据获取失败"
							})
						}
						this.swipers = res.data.message
					}
				})
			}
		}
	}
</script>

<style>
	
</style>
