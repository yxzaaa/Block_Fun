<template>
	<view class="container">
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="选择收货地址"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
		/>
		<view class="app-container full fixbutton">
			<block v-for="(item,index) in addressList" :key="item.id">
				<view class="tosite" :style="{borderBottom:index === addressList.length-1?'none':'1px solid rgba(255,255,255,0.1)'}">
					<view class="site" @click="setAddresss(item)">
						<span class="person-info">
							<span class="name-phone">
								<span class="name" style="font-size:28upx;color:#fff;">{{item.truename}}</span>
								<span class="phone" style="font-size:24upx;color:#999999;">{{item.mobile}}</span>
							</span>
							<span class="adress" style="font-size:24upx;display: block;color:#999999;">{{item.full}}</span>
						</span>
					</view>
					<span style="border-left:1px solid rgba(255,255,255,0.4);display: block;padding-left:30upx;font-size:24upx;color:#DA53A2;" @click="editAddress(item)">编辑</span>
				</view>
			</block>
			<view class="fixed-buttons">
				<view class="button-group">
					<fun-button value="创建新地址" width="670upx"  large url="../address/addressManage?delta=2"></fun-button>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import UniBackground from '@/components/uni-background/uni-background.vue';
	import UniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue';
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
				},
				addressList:[]
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onShow(){
			//获取收货地址列表
			this.$http({
				url:'/member/address',
				success:res=>{
					console.log(res);
					this.addressList = res.data;
				}
			})
		},
		methods:{
			setAddresss(item){
				uni.setStorage({
					key:'currAddress',
					data:{
						truename:item.truename,
						mobile:item.mobile,
						full:item.full,
					},
					success:()=>{
						uni.navigateBack({
							delta:1
						})
					}
				})
			},
			editAddress(item){
				uni.setStorage({
					key:'currEditAddress',
					data:item,
					success:()=>{
						uni.navigateTo({
							url:'../editAddress/editAddress'
						})
					}
				})
			}
		}
	}

		
	
</script>

<style lang="scss" scoped>
	.tosite{
		width:750upx;
		padding:40upx;
		border-bottom:1px solid rgba(255,255,255,0.1);
		display:flex;
		align-items:center;
		justify-content:space-between;
		&:active{
			opacity: 0.8;
		}
		.site{
			display: flex;
			align-items: center;
			.person-info{
				margin-left:20upx;
				width:500upx;
				.phone{
					margin-left:20upx;
				}
			}
			.toaddress{
				color:#fff;
				font-size:28upx;
				margin-left:32upx;
			}
		}
		
	}
	.button-group{
		width:670upx;
	}
</style>
