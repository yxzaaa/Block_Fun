<template>
	<view class="container">
		<uni-background src="../../static/bg1.jpg"/>
		<uni-nav-bar :title="currType == 1?'发布借贷挂单':'发布投资挂单'" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<div class="app-container full fixbutton" style="padding-bottom:190upx;">
			<view class="modal-box" v-if="showPwdModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">请输入您的交易密码</view>
						<view class="modal-content">
							<password-inputer @input="setPassword" :value="password"></password-inputer>
						</view>
					</view>
					<view class="modal-btns">
						<view @click="showPwdModal = false">取消</view>
						<view style="border-left:1px solid #eee;color:#0A61C9;" @click="publish">发布</view>
					</view>
				</view>
			</view>
			<view class="modal-box" v-if="showModal">
				<view class="modal">
					<view class="modal-top-item">
						<view class="modal-title">预计放款金额</view>
						<view class="modal-content">
							<view style="font-size: 24upx;padding-top:10upx;text-align: left;">1.质押率：Forest 的质押率为 50%，即放款比例为本金的50%；</view>
							<view style="font-size: 24upx;padding-top:10upx;text-align: left;">2.补仓线：Forest 的补仓线为 75%，抵押市值到达 75% 后，会通知借款方补仓；</view>
							<view style="font-size: 24upx;padding-top:10upx;text-align: left;">3.平仓线：Forest 的平仓线为 60%，抵押市值到达 60% 后，投资人有权进行平仓；</view>
						</view>
					</view>
					<view class="modal-btns">
						<view style="border-left:1px solid #eee;color:#0A61C9;width:100%;" @click="showModal = false">关闭</view>
					</view>
				</view>
			</view>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button  
						value="立即发布" 
						width="670upx"  
						large 
						@handle="showPwdModal = true"
					></fun-button>
				</view>
				<view class="certs">
					<image :src="checkCert?imageLib.certChecked:imageLib.certCheck" class="check-cert"></image>
					<span class="cert-text">我已经阅读并同意 <span class="cert-name">《用户协议》</span> 和 <span class="cert-name">《质押合同》</span></span>
				</view>
			</view>
			<view class="user-count" style="padding-top:20upx;">
				<text style="font-family: 'Montserrat-Bold';font-size:64upx;">{{getTotalPrice()}}</text>
				<text>USDT</text>
			</view>
			<view class="user-info" @click="showInfo">
				<text style="color:rgba(255,255,255,0.5);font-size: 26upx;">预计放款金额</text>
				<image style="width:36upx;height:36upx;margin-left:8upx;" :src="imageLib.info"></image>
			</view>
			<view style="padding:40upx;">
				<view class="fun-card">
					<view class="fun-card-item">
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">交易类型</text>
							</view>
							<view class="right-item" style="width:272upx;">
								<view class="radio-box">
									<text style="width:50%;" :class="{'active':currType == 1}" @click="currType = 1">借款</text>
									<text style="width:50%;" :class="{'active':currType == 2}" @click="currType = 2">投资</text>
								</view>
							</view>
						</view>
						<!-- <view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">投资总量</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">800 USDT</text>
							</view>
						</view> -->
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押币种</text>
							</view>
							<view class="right-item">
								<picker @change="coinChange" :value="currCoin" :range="coinLib" mode="selector">
									<view 
									style="padding:0upx 20upx;border-radius: 6upx;height:100%;background: #2D1F25;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;">
										<text style="#999;">{{coinLib[currCoin]}}</text>
										<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;"></image>
									</view>
								</picker>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">USDT价格</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{publicLib[currCoin]?publicLib[currCoin].unit_price:''}} USDT{{coinLib[currCoin] == 'USDT'?'':'/'+coinLib[currCoin]}}</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押单价</text>
							</view>
							<view class="right-item">
								<input v-model="price" style="font-size: 26upx;color:#fff;text-align: right;" type="number" placeholder="请输入抵押单价" placeholder-style="font-size:24upx;"/>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押总量</text>
							</view>
							<view class="right-item">
								<input v-model="totalCount" style="font-size: 26upx;color:#fff;text-align: right;" type="number" placeholder="请输入抵押总量" placeholder-style="font-size:24upx;"/>
							</view>
						</view>
						<!-- <view style="width:100%;height:3upx;background:rgba(255,255,255,0.2);margin:20upx 0upx;"></view> -->
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">抵押周期</text>
							</view>
							<view class="right-item" style="height:48upx;">
								<picker @change="pickerChange" :value="currClass" :range="classLib" range-key="name" mode="selector">
									<view 
									style="padding:0upx 20upx;border-radius: 6upx;height:100%;background: #2D1F25;line-height: 48upx;color:#fff;display: flex;justify-content: center;align-items: center;">
										<text style="#999;">{{classLib[currClass].name}}</text>
										<image :src="imageLib.sanjiao" style="width:20upx;height:14upx;"></image>
									</view>
								</picker>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">月利率</text>
							</view>
							<view class="right-item">
								<input v-model="rate" style="font-size: 26upx;color:#fff;text-align: right;" type="number" placeholder="请输入月利率" placeholder-style="font-size:24upx;"/><span class="symble">%</span>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">预计利息</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{getPreRate()}} USDT</text>
							</view>
						</view>
						<view class="horizon-list-item">
							<view class="left-item">
								<text class="left-item-label">手续费</text>
							</view>
							<view class="right-item">
								<text class="left-item-name">{{fee}} USDT</text>
							</view>
						</view>
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
	import PasswordInputer from '@/components/possword-inputer.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			FunButton,
			PasswordInputer
		},
		data() {
			return {
				scroll:0,
				showModal:false,
				showPwdModal:false,
				checkCert:true,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					}
				},
				imageLib:{
					info:'../../static/icons/icon_info.png',
					sanjiao:'../../static/icons/sanjiao.png',
					certCheck:'../../static/icons/cert_check.png',
					certChecked:'../../static/icons/cert_checked.png',
				},
				userInfo:{
					avatar:'../../static/avatar/fortoken.png',
					username:'Xdog',
					usercount:'+8089.23'
				},
				currClass:0,
				currCoin:0,
				classLib:[
					{
						value:3,
						name:'3月'
					},
					{
						value:6,
						name:'6月'
					},
				],
				coinLib:[],
				publicLib:[],
				fee:0,
				mortgage:0,
				price:'',
				totalCount:'',
				totalPrice:0,
				preRate:0,
				rate:'',
				currType:1,
				password:''
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			//请求币种和参考价格
			this.$http({
				url:'/v1/main/debit/debit-preloading',
				success:res=>{
					console.log(res);
					if(res.code == 200){
						res.data.coin.map(item=>{
							this.coinLib.push(item.coin);
						});
						this.publicLib = res.data.coin;
						this.fee = res.data.fee;
						this.mortgage = res.data.mortgage;
					}
				}
			})
		},
		methods:{
			setPassword(val){
				this.password = val;
			},
			//发布挂单
			publish(){
				if(this.currType == 1){
					//发布借款挂单
					this.$http({
						url:'/v1/main/debit/debit-loan-request',
						data:{
							coin: this.coinLib[this.currCoin],
							price: this.price,
							amount: this.totalPrice,
							rate: this.rate/100,
							month: this.classLib[this.currClass].value,
							password: this.password
						},
						success:res=>{
							console.log(res);
							if(res.code == 200){
								uni.showToast({
									title:'发布成功',
									icon:'none'
								})
								uni.navigateBack({
									delta:1
								})
							}else{
								uni.showToast({
									title:res.message,
									icon:'none'
								})
							}
						}
					})
				}else{
					//发布投资挂单
					this.$http({
						url:'/v1/main/debit/debit-investment-request',
						data:{
							coin: this.coinLib[this.currCoin],
							price: this.price,
							amount: this.totalPrice,
							rate: this.rate/100,
							month: this.classLib[this.currClass].value,
							password: this.password
						},
						success:res=>{
							console.log(res);
							if(res.code == 200){
								uni.showToast({
									title:'发布成功',
									icon:'none'
								})
								uni.navigateBack({
									delta:1
								})
							}else{
								uni.showToast({
									title:res.message,
									icon:'none'
								})
							}
						}
					})
				}
			},
			getTotalPrice(){
				var price = this.price == ''?0:this.price;
				var count = this.totalCount == ''?0:this.totalCount;
				var unit_price = this.publicLib[this.currCoin].unit_price;
				this.totalPrice = (parseFloat(price)*parseInt(count)/2).toFixed(2);
				return (parseFloat(price)*parseInt(count)*parseFloat(unit_price)/2).toFixed(2);
			},
			getPreRate(){
				 var price = this.price == ''?0:this.price;
				 var count = this.totalCount == ''?0:this.totalCount;
				 var rate =  this.rate == ''?0:this.rate;
				 var month = this.classLib[this.currClass].value;
				 return ((parseFloat(price)*parseInt(count)/2)*parseFloat(rate)*month/100).toFixed(2);
			},
			pickerChange(e){
				this.currClass = e.target.value;
			},
			coinChange(e){
				this.currCoin = e.target.value;
			},
			showInfo(){
				this.showModal = true;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.radio-box{
		border-radius: 10upx;
		overflow: hidden;
		margin:0px;
		text{
			border-radius: 0px;
		}
	}
	.symble{
		margin-left:10upx;
		color:#999;
	}
	.user-info{
		width:230upx;
		margin:auto;
		display:flex;
		justify-content:center;
		align-items:center;
		padding:10upx 0;
		image{
			width:48upx;
			height:48upx;
		}
		text{
			color:#fff;
			font-size: 32upx;
		}
	}
	.user-count{
		width:750upx;
		text-align:center;
		padding:10upx 0;
		text{
			color:#fff;
			font-size: 44upx;
			padding:0px 10upx;
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
	.horizon-list-item{
		padding:16upx 0upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		.left-item{
			display:flex;
			justify-content:flex-start;
			align-items:center;
			.left-item-avatar{
				width:40upx;
				height:40upx;
				margin-right:20upx;
			}
			.left-item-name{
				color:#fff;
				font-size: 26upx;
				padding-right:15upx;
			}
			.left-item-label{
				color:#999;
				font-size: 24upx;
				margin-right: 18upx;
			}
			.left-item-title{
				display: block;
				color:#fff;
				font-size: 32upx;
				line-height: 52upx;
				font-family:'Montserrat-Bold';
				span{
					font-family:'Montserrat-Bold';
				}
			}
			.left-item-date{
				display: block;
				color:#999;
				font-size: 26upx;
				line-height: 52upx;
				font-family:'Montserrat-Light';
			}
		}
		.right-item{
			display:flex;
			justify-content:flex-end;
			align-items:center;
			color:#999;
			font-size: 24upx;
			.left-item-name{
				color:#fff;
				font-size: 26upx;
			}
			.right-item-text{
				font-size: 38upx;
				color:#56CCF2;
				font-family:'Montserrat-Bold';
				span{
					font-family:'Montserrat-Bold';
				}
			}
			image{
				width:42upx;
				height:42upx;
				margin-left:10upx;
			}
		}
	}
</style>
