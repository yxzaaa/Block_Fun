<template>
	<view class="container">
		<uni-background />
		<uni-nav-bar :title="coin+' Wallet 钱包'" textColor="#fff" :opacity="scroll" layout="center" :buttons="navButtons"></uni-nav-bar>
		<view class="app-container full">
			<view class="horizon-tab">
				<horizon-tab :tabs="navTabs" padding="40" @click="updateList"/>
			</view>
			<view class="horizon-list">
				<block v-for="(item,index) in xdogList" :key="index">
					<view class="horizon-list-item" @click="toDetail(item)">
						<view class="left-item">
							<text class="left-item-title">{{getTranId(item.tid)}}</text>
							<text class="left-item-date">{{getDate(item.modified_on)}}</text>
						</view>
						<view class="right-item">
							<span class="right-item-text" :style="{color:item.type == 1?'#DA53A2':item.type == 2?'#56CCF2':'#F2C94C'}">
								<span>{{item.type == 1?'!':item.type == 2?'+':'-'}}</span>
								{{item.amount}}
							</span>
							<image :src="imageLib.more"></image>
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
	import HorizonTab from '@/components/horizon-tab.vue';
	export default {
		components:{
			UniNavBar,
			UniBackground,
			HorizonTab
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
				imageLib:{
					more:'../../static/icons/more.png'
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
				xdogList:[
					// {
					// 	tid:'o43fdksok4kf4o2342lk324fdskeo',
					// 	modified_on:'1568834690',
					// 	type:1,
					// 	amount:'50.34',
					// }
				],
				coin:'',
			};
		},
		onLoad(option){
			this.coin = option.coin;
			this.updateList(0);
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		methods:{
			//更新转账记录
			updateList(index){
				this.$http({
					url:'/v1/main/account/bill-history',
					data:{
						coin:this.coin,
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							this.xdogList = [];
							var data = res.data.bill_info;
							if(data){
								data.map(item=>{
									if(item.status == this.navTabs[index].id){
										this.xdogList.push(item);
									}
								})
							}
						}
					}
				})
			},
			toDetail(item){
				uni.setStorage({
					key:'trans_detail_info',
					data:item,
					success:res=>{
						uni.navigateTo({
							url:'../xdogdetail/xdogdetail'
						})
					}
				})
			},
			//获取交易号
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
	.horizon-list{
		padding:40upx 0upx;
		.horizon-list-item{
			padding:20upx 40upx;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.left-item{
				width:400upx;
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
				image{
					width:42upx;
					height:42upx;
					margin-left:10upx;
				}
			}
		}
	}
</style>
