<template>
	<view>
		<view>
			数据绑定和vue相同
		</view>
		<view>{{msg}}</view>
		<image :src="imgUrl" mode=""></image>
		<view v-for="(item, index) in arr" :key="index">
			名字：{{item.name}}: 年龄：{{item.age}}
		</view>
		
		<button type="default" v-on:click="clickHandle(20,$event)">按钮</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				msg: "hhhhhhhello",
				imgUrl: "https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1603705321&di=4f1d10460d87920d8540af818380ba03&src=http://a3.att.hudong.com/64/52/01300000407527124482522224765.jpg",
				arr: [
					{
						name:"xiao1",
						age: 20
					},
					{
						name:"xiao2",
						age: 21
					},
					{
						name:"xiao3",
						age: 22
					},
					{
						name:"xiao4",
						age: 23
					}
				]
			};
		},
		methods:{
			clickHandle:function(id, e){
				console.log("点击事件"+ id,e)
			}
		}
	}
</script>

<style lang="scss">

</style>
