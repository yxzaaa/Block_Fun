<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar title="收款方式" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons" @handle="handleButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="horizon-list">
				<block v-for="(item,index) in payMethods" :key="index">
					<view class="horizon-list-item">
						<view class="left-item">
							<image :src="item.icon" class="left-item-avatar"></image>
							<text class="left-item-title">{{item.name}}</text>
						</view>
						<view class="right-item">
							<image :src="imageLib.check" v-if="item.status == 'canUse' && item.checked == 0 && !editing" @click="setChecked(index)"></image>
							<image :src="imageLib.checked" v-if="item.status == 'canUse' && item.checked == 1 && !editing"></image>
							<text v-if="item.status == 'noUse' || editing" :style="{color:item.status == 'noUse'?'#fff':'rgba(255,255,255,0.5)'}" @click="editPay(item.name)">{{item.status == 'noUse'?'未填写':'已填写'}}</text>
							<image :src="imageLib.more" v-if="item.status == 'noUse' || editing"></image>
						</view>
					</view>
				</block>
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
			UniBackground
		},
		data() {
			return {
				scroll:0,
				editing:false,
				navButtons:{
					back:{
						type:'normal',
						text:'取消'
					},
					setting:{
						type:'normal',
						text:'handle',
						classify:'setting'
					}
				},
				imageLib:{
					checked:'../../static/bg/check.png',
					check:'../../static/bg/checkbox.png',
					more:'../../static/icons/more.png'
				},
				payMethods:[
					{
						id:1,
						name:'微信',
						status:'canUse',
						checked:1,
						icon:'../../static/icons/icon_wechatpay_light.png'
					},
					{
						id:2,
						name:'支付宝',
						status:'canUse',
						checked:0,
						icon:'../../static/icons/icon_alipay_light.png'
					},
					{
						id:3,
						name:'银行卡',
						status:'noUse',
						checked:0,
						icon:'../../static/icons/icon_bankcard.png'
					},
				]
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			setChecked(id){
				this.payMethods.map(item=>{
					item.checked = 0;
				});
				this.payMethods[id].checked = 1;
			},
			handleButtons(res){
				if(res == 'setting'){
					this.editing = this.editing?false:true;
				}
			},
			editPay(name){
				uni.navigateTo({
					url:'../editpaymethod/editpaymethod?name='+name
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.horizon-list{
		padding:40upx 0upx;
		padding-top:0px;
		.horizon-list-item{
			padding:20upx 40upx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.left-item{
				width:400upx;
				display:flex;
				justify-content:flex-start;
				align-items:center;
				.left-item-avatar{
					width:48upx;
					height:48upx;
					margin-right:30upx;
				}
				.left-item-title{
					display: block;
					color:#fff;
					font-size: 28upx;
					line-height: 52upx;
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
				width:300upx;
				display: flex;
				justify-content: flex-end;
				align-items: center;
				.right-item-text{
					font-size: 38upx;
					color:#56CCF2;
					font-family:'Montserrat-Bold';
					span{
						font-family:'Montserrat-Bold';
					}
				}
				text{
					color:#fff;
					font-size: 28upx;
				}
				image{
					width:42upx;
					height:42upx;
					margin-left:10upx;
				}
			}
		}
	}
</style>
