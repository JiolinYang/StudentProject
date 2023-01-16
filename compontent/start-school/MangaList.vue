<template>
	<view class="manga-list">
		<view class="list-item">
			<image class="item-bg" src="../../static/imgs/archives.png" mode=""></image>
			<view class="item-text">档案管理</view>
		</view>
		<view class="list-item">
			<image class="item-bg" :src="signList.imgUrl" mode=""></image>
			<view class="item-text">{{signList.name}}</view>
		</view>
		<view class="list-item">
			<image class="item-bg" :src="mangaList.imgUrl" mode=""></image>
			<view class="item-text">{{mangaList.name}}</view>
		</view>
		<view class="list-item" @tap="goHelp">
			<image class="item-bg" src="../../static/imgs/service.png" mode=""></image>
			<view class="item-text" >咨询帮助</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				mangaList:{
					imgUrl:'../../static/imgs/sign-out.png',
					name:'签署协议'
				},
				signList:{
					imgUrl:'../../static/imgs/sign-in.png',
					name:'我的协议'
				}
			}
		},
		methods:{
			goHelp(){
				uni.navigateTo({
					url:'../../pages/consulting-help/consulting-help'
				})
			}
		}
	}
</script>

<style scoped>
	.manga-list{
		display: flex;
		justify-content: space-between;
		align-items: center;
		box-sizing: border-box;
	}
	.item-bg{
		width: 108rpx;
		height: 108rpx;
	}
	.item-text{
		width: 108rpx;
		height: 25rpx;
		font-size: 26rpx;
		font-weight: 400;
		color: #222222;
		padding-top: 10rpx;
	}
</style>
