<template>
	<view>
		<view>
			<text selectable>你好啊</text>
		</view>
		<view><text>你好啊</text></view>
		<view><text class="t" space="nbsp">你    好啊</text></view>
		
		<view>
			<text decode>&gt;</text>
		</view>
	
		<view class="box2" hover-class="box-active2" hover-start-time="3000">
			<view class="box" hover-class="box-active" hover-stop-propagation hover-stay-time="2000">我是大盒子</view>
		</view>
		
		<button size="default" type="default">默认按钮</button>
		<button size="mini" type="primary" plain>小按钮</button>
		<button size="mini" type="warn" plain disabled>小按钮</button>
		<button size="mini" type="primary" plain loading>加载小按钮</button>
		
		<image src="../../static/index.png" mode=""></image>
		<image src="../../static/index.png" mode="aspectFit"></image>
		<image src="../../static/index.png" mode="aspectFill"></image>
	</view>
	
	
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.t{
	font-size: 20px;
}

.box{
	width: 100px;
	height: 100px;
	background-color: green;
}

.box2{
	width: 200px;
	height: 200px;
	background-color: #333333;
}

.box-active{
	background-color: #007AFF;
}

.box-active2{
	background-color: pink;
}
</style>
