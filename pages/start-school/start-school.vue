<template>
	<view class="start-school">
		<MyHeader :title ="title"></MyHeader>
		<scroll-view scroll-y="true">
			<view>
				<!-- 顶部填写入学信息 -->
				<view class="banner-bg">
					<view class="sign-btn" @tap="goEnterSchool">立即填写 > </view>
				</view>
				<view class="school-content">
					<!-- 按钮列表 -->
					<MangaList></MangaList>
					<!-- 名人堂 -->
					<view class="main-title">名人堂</view>
					<scroll-view scroll-x="true" class="scroll-content">
						<view class="scroll-item">
							<CelebrityList :excellentList='excellentList'></CelebrityList>
						</view>
					</scroll-view>
					<!-- 公告 -->
					<view class="main-title">公告</view>
					<Notice :noticeList='noticeList'></Notice>
					<!-- <Notice></Notice> -->
				</view>
			</view>
		</scroll-view>
		<!-- 弹窗  快速入学 -->
		<view class="pop" v-if="isPop">
			<view class="pop-mask"></view>
			<view class="pop-box">
				<view class="pop-content">
					<image class="close" @tap="closePop" src="../../static/imgs/close.png" mode=""></image>
					<image class="pop-btn" src="../../static/imgs/pop-btn.png" mode=""></image>
					<view class="btn-text" @tap="goEnterSchool">快速入学</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import MyHeader from '@/common/my-header/my-header.vue'
	import MangaList from '@/compontent/start-school/MangaList.vue'
	import CelebrityList from '@/compontent/start-school/CelebrityList.vue'
	import Notice from '@/compontent/start-school/Notice.vue'
	import { excellentList,noticeList } from '@/servies/start-school.js'
	
	export default{
		data(){
			return{
				title:'',
				isPop:true,
				pageNum:1,
				pageSize:10,
				excellentList:[],
				noticeList:[]
			}
		},
		onLoad(options) {
			const item = JSON.parse(options.item)
			this.title = item.className
			this.__init()
		},
		methods:{
			// 获取名人堂信息
			async __init(){
				const data = {
					pageNum:this.pageNum,
					pageSize:this.pageSize
				}
				this.excellentList = await excellentList(data)
				// console.log( this.excellentList )
				this.noticeList = await noticeList(data)
				console.log( this.noticeList )
			},
			// 关闭快速入学
			closePop(){
				this.isPop = false
			},
			// 跳转到入学信息填写的页面
			goEnterSchool(){
				uni.navigateTo({
					url:'../enter-school/enter-school'
				})
			}
		},
		components:{
			MyHeader,
			MangaList,
			CelebrityList,
			Notice
		}
	}
</script>

<style scoped>
	/* 消除滚动条 */
	scroll-view ::-webkit-scrollbar{
		display: none;
		width: 0 !important;
		height: 0 !important;
		-webkit-appearance:none;
		background: transparent;
		color: transparent;
	}
	scroll-view{
		height: 1500rpx;
		background-color: #f3f4f6;
	}
	.start-school{
		width: 100vw;
		height: 100vh;
		box-sizing: border-box;
		background-color: #f3f4f6;
	}
	/* 顶部立即填写 */
	.banner-bg{
		position: relative;
		width: 750rpx;
		height: 295rpx;
		background: url('https://fawn.xuexiluxian.cn/api/profile/wechat/bgimg/banner.png') no-repeat;
		background-size: contain;
	}
	.sign-btn{
		position: absolute;
		top: 195rpx;
		left: 60rpx;
		width: 173rpx;
		height: 44rpx;
		font-size: 28rpx;
		color: #FFFFFF;
		padding: 5rpx 10rpx;
		text-align: center;
		line-height: 44rpx;
		border: 1rpx solid #FFFFFF;
		border-radius: 40rpx;
	}
	.school-content{
		padding: 40rpx 37rpx;
	}
	.main-title{
		width: 102rpx;
		height: 33rpx;
		font-size: 34rpx;
		font-weight: bold;
		color: #252525;
		margin-top: 54rpx;
		margin-bottom: 36rpx;
	}
	.scroll-content{
		width: 100%;
		height: 100%;
	}
	.scroll-item{
		display: inline-block;
	}
	/* 快速入学 */
	.pop{
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 9999;
	}
	.pop-mask{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0,0,0,.3);
	}
	.pop-box{
		width: 500rpx;
		height: 700rpx;
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%,-50%);
	}
	.pop-content{
		width: 500rpx;
		height: 693rpx;
		background: url('https://fawn.xuexiluxian.cn/api/profile/wechat/bgimg/pop-bg.png') no-repeat;
		background-size: contain;
	}
	.close{
		width: 63rpx;
		height: 63rpx;
		position: absolute;
		right: -20rpx;
		top: -20rpx;
	}
	.pop-btn{
		width: 420rpx;
		height: 80rpx;
		position: absolute;
		left: 45rpx;
		bottom: 126rpx;
	}
	.btn-text{
		width: 136rpx;
		height: 33rpx;
		font-size: 34rpx;
		font-weight: bold;
		color: #FFFFFF;
		position: absolute;
		left: 185rpx;
		bottom: 160rpx;
	}
</style>
