<template>
	<view class="container">
		<uni-background :src="imageLib.bg"/>
		<uni-nav-bar 
			:opacity="scroll"
			title="我的"
			textColor="#fff"
		/>
		<view class="app-container full">
			<view class="user-info">
				<image src="../../static/bg/logo.png" style="width:124upx;height:124upx;"></image>
				<view class="info">
					<span class="id">{{userInfo.login_name}}</span>
					<span class="users" style="margin-top:20upx;">
						<span class="user" style="margin-right:44upx;font-size:24upx;font-family: Montserrat-bold;color:#999999;">
							UID：{{userInfo.uid.substring(0,16)+'...'}}
						</span>
						<span style="font-size:24upx;color:#999999;border:1px solid #999999;padding:4upx 24upx;border-radius:6upx;">一键复制</span>
					</span>
				</view>
			</view>
			<view class="activity">
				<view class="active">
					<view>
						<image src="../../static/bg/task.png"></image>
						<span>每日任务</span>
					</view>
					<view>
						<image src="../../static/bg/friends.png"></image>
						<span>我的好友</span>
					</view>
					<view>
						<image src="../../static/bg/invite.png"></image>
						<span>邀请好友</span>
					</view>
				</view>
			</view>
			<view class="managebox">
				<!-- 点击跳转到订单管理页面 -->
				<navigator url="../order-manage-all/order-manage-all">
					<view class="manage">
						<span class="title">订单管理</span>
						<view>
							<span class="goodsinfo">
								<span class="number">{{orderNum}}</span>
								<span class="text">条订单信息</span>
							</span>
							<image src="../../static/bg/message.png" style="width:72upx;height:72upx;"></image>
						</view>
					</view>
				</navigator>
				<!-- 点击跳转到购物车页面 -->
				<navigator url="../cart1/cart1">
					<view class="manage">
						<span class="title">购物车</span>
						<view>
							<span class="goodsinfo">
								<span class="number">{{cartNum}}</span>
								<span class="text">条商品信息</span>
							</span>
							<image src="../../static/bg/cart.png" style="width:72upx;height:72upx;"></image>
						</view>
					</view>
				</navigator>	
			</view>
			<view class="managebox">
				<navigator url="../favorite/favorite">
					<view class="manage">
						<span class="title">收藏夹</span>
						<view>
							<span class="goodsinfo">
								<span class="number">{{saveNum}}</span>
								<span class="text">条收藏信息</span>
							</span>
							<image src="../../static/bg/sign.png" style="width:72upx;height:72upx;"></image>
						</view>
					</view>
				</navigator>
				<view class="manage">
					<span class="title">在线客服</span>
					<view>
						<span class="goodsinfo">
							<span class="number">0</span>
							<span class="text">条客服信息</span>
						</span>
						<image src="../../static/bg/service.png" style="width:72upx;height:72upx;"></image>
					</view>
				</view>
			</view>
			<view class="action">
				<navigator url="../finance/finance">
					<view class="action-item">
						<view>
							<image src="../../static/bg/finance.png"></image>
							<span>我的财务</span>
						</view>
						<image src="../../static/bg/jiantou.png"></image>
					</view>
					<view class="item-horizen"></view>
				</navigator>
				<navigator url="../realname-attest/realname-attest">
					<view class="action-item">
						<view>
							<image src="../../static/bg/realname.png"></image>
							<span>实名认证</span>
						</view>
						<image src="../../static/bg/jiantou.png"></image>
					</view>
					<view class="item-horizen"></view>
				</navigator>
				<navigator url="../security/security">
					<view class="action-item">
						<view>
							<image src="../../static/bg/save.png"></image>
							<span>安全中心</span>
						</view>
						<image src="../../static/bg/jiantou.png"></image>
					</view>
					<view class="item-horizen"></view>
				</navigator>
				<navigator url="../helpcenter/helpcenter">
					<view class="action-item">
						<view>
							<image src="../../static/bg/help.png"></image>
							<span>帮助中心</span>
						</view>
						<image src="../../static/bg/jiantou.png"></image>
					</view>
					<view class="item-horizen"></view>
				</navigator>
				<navigator url="../aboutus/aboutus">
					<view class="action-item" style="border:none;margin-bottom: 0;">
						<view>
							<image src="../../static/bg/about.png"></image>
							<span>关于我们</span>
						</view>
						<image src="../../static/bg/jiantou.png"></image>
					</view>
				</navigator>
			</view>
			<view class="exit" @click="logout">
				退出登录
			</view>		
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
				imageLib:{
					bg:'../../static/bg2.jpg'
				},
				userInfo:{},
				orderNum:0,
				saveNum:0,
				cartNum:0,
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onShow(){
			//获取用户信息
			this.$http({
				url:'/v1/main/users/user-info',
				success:res=>{
					if(res.code == 200){
						this.userInfo = res.data;
					}
				}
			})
			//获取我的信息
			this.$http({
				url:'/member/my',
				success:res=>{
					if(res.code == 200){
						this.orderNum = res.data.order;
						this.cartNum = res.data.cart;
						this.saveNum = res.data.favorite;
					}
				}
			})
		},
		methods:{
			logout(){
				uni.removeStorage({
					key:'userInfo',
					success:res=>{
						uni.reLaunch({
							url:'../login/login'
						})
					}
				})
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	.user-info{
		display: flex;
		width:750upx;
		padding:0px 40upx;
		height:124upx;
		justify-content:flex-start;
		.info{
			display: flex;
			flex-direction: column;
			padding-left:30upx;
			.id{
				font-family: Montserrat-bold;
				font-style: normal;
				font-weight: 600;
				font-size: 32upx;
				color:#fff;
				padding-top:8upx;
			}
		}
	}
	.activity{
		width:670upx;
		height:180upx;
		margin:64upx 40upx 0;
		background-image:url(../../static/bg3.jpg);
		background-size:100% 100%;
		border-radius: 12upx;
		padding:28upx 64upx 22upx;
		.active{
			display: flex;
			justify-content:space-between;
			
			view{
				display: flex;
				flex-direction: column;
				justify-content:center;
				
				image{
					margin-left:2upx;
					width:88upx;
					height:88upx;
					margin-bottom: 8upx;
				}
				span{
					font-size:24upx;
					color: #DA53A2;
				}
				
			}
		}
		
	}
	.managebox{
		width:670upx;
		height:200upx;
		margin:40upx 40upx 30upx;
		display:flex;
		justify-content:space-between;
		.manage{
			background: rgba(45, 31, 37,.8);
			padding:40upx;
			width:324upx;
			height:200upx;
			border-radius:8upx;
			.title{
				
				font-size: 28upx;
				color:#fff;
				font-weight: bold;
			}
			view{
				display: flex;
				justify-content:space-between;
				align-items: flex-start;
				margin-top:8upx;
				.goodsinfo{
					display: flex;
				}
				.number{
					margin-right:12upx;
					display: block;
					color: #DA53A2;
					font-family: Montserrat-Bold;
					font-style: normal;
					font-weight: 600;
					font-size: 24upx;
				}
				.text{
					color:#999999;
					font-size: 24upx;
				}
			}
		}
	}
	.action{
		width:670upx;
		background: rgba(45, 31, 37,.8);
		border-radius: 8upx;
		margin:40upx 40upx 0;
		.action-item{
			display:flex;
			width:670upx;
			justify-content:space-between;
			padding:40upx 30upx;
			view{
				display:flex;
				justify-content:space-between;
				align-items:center;
				image{
					width:36upx;
					height:36upx;
					margin-top:0px;
					margin-right:40upx;
					
				}
				span{
					font-size:28upx;
					color: #fff;
				}
			}
			image{
				width:26upx;
				height:26upx;
				margin-top: 6upx;
			}
		}
		.item-horizen{
			width:610upx;
			height:2upx;
			background: rgba(255,255,255,0.2);
			margin:0px 30upx;
		}
	}
	.exit{
		width:670upx;
		height:88upx;
		margin:124upx 40upx 190upx;
		background: rgba(45, 31, 37,.8);
		border-radius: 4px;
		text-align: center;
		line-height: 88upx;
		font-size:28upx;
		color:#fff;
	}
</style>
