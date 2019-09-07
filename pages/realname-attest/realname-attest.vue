<template>
	<view>
		<uni-background />
		<uni-nav-bar 
			title="实名认证" 
			textColor="#fff" 
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full">
			<view class="idbox">
				<view class="idcard">
					<view class="cardbox">
						<view>
							<image src="../../static/bg/idcard1.png"></image>
							<span>身份证正面</span>
						</view>
						<view>
							<image src="../../static/bg/idcard2.png"></image>
							<span>身份证反面</span>
						</view>
					</view>
					<view class="person-card">
						<image src="../../static/bg/photo.png"></image>
						<span>手持身份证拍照</span>
					</view>
				</view>
				<view class="idtext">
					<span>身份证姓名</span>
					<input type="text" value="请填写真实姓名">
				</view>
				<view class="idtext" style="margin-top:34upx;">
					<span>身份证号码</span>
					<input type="text" value="请填写15位或18位身份证号">
				</view>
			</view>
			<view class="commit">提交</view>
		</view>
	</view>
	
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
		},
		data() {
			return {
				scroll:0,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},
					
				}
			}
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
	.idbox{
		width:670upx;
		background:#2D1F25;
		border-radius:8upx;
		margin:0upx 40upx 124upx;
		padding:58upx 30upx;
		.idcard{
			display: flex;
			justify-content:space-between;
			.cardbox{
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				view{
					width:290upx;
					height:186upx;
					border-radius:8upx;
					border:1px solid rgba(255,255,255,0.1);
					margin-bottom:30upx;
					margin-right:30upx;
					display:flex;
					flex-direction:column;
					align-items:center;
					justify-content:center;
					image{
						width:40upx;
						height:38upx;
						border:1px dashed rgba(255,255,255,0.5);
						padding:4upx 0;
						margin-bottom: 4upx;
					}
					span{
						font-size: 24upx;
						color: #FFFFFF;
						opacity: 0.5;
					}
				}
			}
			.person-card{
				width:290upx;
				height:400upx;
				border-radius:8upx;
				border:1px solid rgba(255,255,255,0.1);
				display:flex;
				flex-direction:column;
				align-items:center;
				justify-content:center;
				image{
					border:1px dashed rgba(255,255,255,0.5);
					width:48upx;
					height:48upx;
					margin-bottom: 4upx;
				}
				span{
					font-size: 24upx;
					color: #FFFFFF;
					opacity: 0.5;
				}
			}
		}
		.idtext{
			span{
				color:#fff;
				font-size: 28upx;
			}
			input{
				background: #15030B;
				border-radius:10upx;
				width:610upx;
				height:88upx;
				color:#fff;
				opacity: 0.5;
				margin-top:24upx;
				padding:28upx 30upx;
				font-size:24upx;
			}
		}
	}
	.commit{
		width:670upx;
		height:80upx;
		margin:120upx 40upx;
		background:#DA53A2;
		text-align: center;
		line-height:80upx;
		color:#fff;
		font-size: 28upx;
		border-radius: 2000upx;
	}
</style>
