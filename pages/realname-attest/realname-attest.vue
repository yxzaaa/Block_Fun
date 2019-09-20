<template>
	<view class="container">
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
							<image src="../../static/icons/credentials_icon.png"></image>
							<span>身份证正面</span>
						</view>
						<view>
							<image src="../../static/icons/credentials_icon-1.png"></image>
							<span>身份证反面</span>
						</view>
					</view>
					<view class="person-card">
						<image src="../../static/icons/zhaoxiangji.png"></image>
						<span>手持身份证拍照</span>
					</view>
				</view>
				<view class="idtext">
					<span>身份证姓名</span>
					<view class="input-field" style="padding:20upx 30upx;">
						<input style="width:100%;font-size: 26upx;color:#c7c7c7;" placeholder="请填写真实姓名"/>
					</view>
				</view>
				<view class="idtext" style="margin-top:34upx;">
					<span>身份证号码</span>
					<view class="input-field" style="padding:20upx 30upx;">
						<input style="width:100%;font-size: 26upx;color:#c7c7c7;" placeholder="请填写15位或18位身份证号"/>
					</view>
				</view>
			</view>
			<fun-button class="commit" value="提交" block large width="670upx"></fun-button>
		</view>
	</view>
	
</template>

<script>
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import FunButton from '@/components/fun-button.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton
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
		margin:40upx;
		margin-top:0px;
		padding:40upx;
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
				padding-bottom:20upx;
				display: block;
			}
			view.input-field{
				background: #15030B;
				border-radius:8upx;
				color:#fff;
				opacity: 0.5;
				font-size:24upx;
			}
		}
	}
	.commit{
		margin:120upx auto;
	}
</style>
