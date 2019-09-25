<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="账单详情" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full">
			<view class="user-info">
				<image :src="userInfo.avatar"></image>
				<text>{{infos.coin}} Wallet</text>
			</view>
			<view class="user-count">
				<text>{{item.type == 1?'!':item.type == 2?'+':'-'}}{{infos.amount}}</text>
			</view>
			<view class="status-box" style="padding:20upx 40upx;">
				<view class="left-status">
					<text style="font-size:30upx;font-family:'Montserrat-Light';color:#fff;">{{getDate(item.modified_on)}}</text>
					<text style="font-size:26upx;color:#999;">创建日期</text>
				</view>
				<view class="right-status">
					<text style="font-size:30upx;color:#fff;">{{navTabs[infos.status].text}}</text>
					<text style="font-size:26upx;color:#999;">订单状态</text>
				</view>
			</view>
			<view class="fun-card" style="margin:30upx 40upx;width:670upx;">
				<view class="fun-card-item">
					<view class="form-item">
						<view class="form-label">收款方</view>
						<view class="form-value-box">
							<view style="display: flex;justify-content: space-between;">
								<text style="font-size:24upx;color:#999;">{{infos.coin}}</text>
								<fun-button type="text" color="#DA53A2" icon="/static/icons/copy.png" value="复制"></fun-button>
							</view>
							<view style="color:#fff;font-family:'Montserrat-Bold';font-size:24upx;">{{infos.to_address}}</view>
						</view>
					</view>
					<view class="form-item">
						<view class="form-label">付款方</view>
						<view class="form-value-box">
							<view style="display: flex;justify-content: space-between;">
								<text style="font-size:24upx;color:#999;">{{infos.coin}}</text>
								<fun-button type="text" color="#DA53A2" icon="/static/icons/copy.png" value="复制"></fun-button>
							</view>
							<view style="color:#fff;font-family:'Montserrat-Bold';font-size:24upx;">{{infos.from_address}}</view>
						</view>
					</view>
					<view class="form-item">
						<view class="input-field">
							<text style="font-size: 24upx;color:#999;">手续费</text>
							<view>
								<text style="color:#fff;font-size: 28upx;font-family:'Montserrat-Light';">{{infos.fee}}Xdog</text>
								<text style="display: inline-block;font-size:24upx;padding:0upx 20upx;color:#999;font-family:'Montserrat-Light';">|</text>
								<text style="font-size: 24upx;color:#999;font-family:'Montserrat-Light';">{{infos.rate*100}}%</text>
							</view>
						</view>
					</view>
					<view class="form-item" style="padding-bottom: 0px;">
						<text style="font-size: 24upx;color:#999;">备注：{{infos.remark}}</text>
					</view>
				</view>
				<view class="fun-horizen"></view>
				<view class="fun-card-item">
					<view class="status-box">
						<view class="left-status">
							<text style="font-size:28upx;font-family:'Montserrat-Light';color:#fff;">{{getTranId(item.tid)}}</text>
							<text style="font-size:24upx;color:#999;">交易号</text>
						</view>
						<view class="right-status">
							<text style="font-size:28upx;color:#fff;">6868</text>
							<text style="font-size:24upx;color:#999;">区块</text>
						</view>
					</view>
				</view>
				<view class="fun-card-item">
					<view class="erweima">
						<image :src="erweima"></image>
					</view>
				</view>
			</view>
		</div>
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
					}
				},
				erweima:'../../static/image.png',
				userInfo:{
					avatar:'../../static/avatar/fortoken.png',
				},
				navTabs:[
					{
						id:0,
						text:'全部'
					},
					{
						id:1,
						text:'转账中'
					},
					{
						id:2,
						text:'待审核'
					},
					{
						id:3,
						text:'已成功'
					},
					{
						id:4,
						text:'已拒绝'
					},
					{
						id:5,
						text:'已失败'
					},
				],
				infos:{}
			};
		},
		onLoad(){
			//获取账单详情
			uni.getStorage({
				key:'trans_detail_info',
				success:res=>{
					this.infos = res.data;
				}
			})
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			getTranId(tid){
				return tid.substr(0,5) + '***'+tid.substr(-9,9);
			},
			getDate(timestamp){
				var date = new Date(timestamp*1000);
				var year = date.getFullYear();
				var month = date.getMonth() + 1;
				var day = date.getDate();
				var hour = date.getHours();
				var min = date.getMinutes();
				month = month>=10?month:'0'+month;
				day = day>=10?day:'0'+day;
				hour = hour>=10?hour:'0'+hour;
				min = min>=10?min:'0'+min;
				return year+'/'+month+'/'+day+' '+hour+':'+min
			},
		}
	}
</script>

<style lang="scss" scoped>
	.user-info{
		width:750upx;
		display:flex;
		justify-content:center;
		align-items:center;
		padding:20upx 0;
		image{
			width:48upx;
			height:48upx;
			margin-right:20upx;
		}
		text{
			color:#fff;
			font-size: 32upx;
		}
	}
	.user-count{
		width:750upx;
		text-align:center;
		padding:30upx 0;
		text{
			color:#DA53A2;
			font-size: 52upx;
			font-family:'Montserrat-Bold';
		}
	}
	.erweima{
		width:200upx;
		height:200upx;
		background: #fff;
		border-radius: 12upx;
		margin:auto;
		padding:20upx;
		image{
			width:100%;
			height:100%;
		}
	}
</style>
