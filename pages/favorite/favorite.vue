<template>
	<view>	
		<uni-background /> <!-- 背景色-->
		<!-- 导航栏 -->
		<uni-nav-bar 	
			title="收藏夹"
			textColor="#fff"
			:opacity="scroll"
			:buttons="navButtons"
			@handle="changeManage"
		/>
		<view class="app-container fixbutton full">
			<view class="guess">
				<view class="guess-list">
					<view 
						v-for="(item, index) in guessList" :key="index"
						class="guess-item"		
					>
					<!-- 引入图片 -->
						<view style="line-height: 160upx;padding-right:40upx;" v-if="isManager" @click="itemChoose(index)">
							<image
								:src="item.isActive?imageLib.checked:imageLib.check" 
								style="width:40upx;height:40upx;"
							></image>
						</view>
						<view class="image-wrapper">
							<image 
								:src="item.src" 
								mode="aspectFill"
								style="width:160upx;height:160upx;"
							></image>
						</view>
						<!-- 图片描述 -->
						<view class="guess-content" :style="{marginLeft:'20upx',marginTop:'0',width:isManager?'420upx':'500upx'}">
							<span style="font-size: 28upx;color:#fff;">{{item.title.substring(0,36)+' ...'}}</span>
							<text style="font-size:24upx;color:#999999;margin-top:4upx;">{{item.consume}} {{item.amount}}</text>
							<span style="color:#DA53A2;">
								<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.symbol}}</span>
								<span style="display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
								<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
							</span>
						</view>
					</view>
				</view>
			</view>
			<view class="fixed-buttons" v-if="isManager">
				<view class="button-group">
					<view class="check" @click="chooseAll">
						<image :src="isChooseAll?imageLib.checked:imageLib.check"></image>
						<span>全选</span>
					</view>
					<fun-button value="删除" width="240upx"></fun-button>
				</view>
			</view>
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
					textbtn:{
						text:"管理",
						type:'handle',
					},
					
				},
				imageLib:{
					checked: '../../static/bg/check.png',
					check:'../../static/bg/checkbox.png',
				},
				guessList: [{
						src: '../../static/bg/p30.png',
						isActive:false,
						title: 'Apple iPhone X (A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'6444.13',
						number:'0'
					},
					{
						src: '../../static/bg/p30.png',
						isActive:false,
						title: '华为P30 (A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'4999.21',
						number:'0',
					},
					{
						src: '../../static/bg/apple.png',
						isActive:false,
						title: 'Apple iPhone X(A1865) 256GB 深空灰色 移动联通电信4G手机',
						consume:'消耗积分',
						amount:'4000',
						symbol:"￥",
						price:'4999.21',
						number:'0',
					},
				],
				isManager:false,
				isChooseAll:false,
				data:{
					guessList:[{},{}],
				}
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.$http({
				url:'/member/favorite',
				success:res=>{
					console.log(res)
				}
			})
		},
		methods:{
			changeManage(){
				if(this.isManager){
					this.isManager = false;
					this.navButtons.textbtn = {
						text:"管理",
						type:'handle',
					}
				}else{
					this.isManager = true;
					this.navButtons.textbtn = {
						text:"完成",
						type:'handle',
					}
				}
			},
			itemChoose(index){
				if(this.guessList[index].isActive){
					this.guessList[index].isActive = false;
				}else{
					this.guessList[index].isActive = true;
				}
				var isAll = true;
				this.guessList.map(item=>{
					if(item.isActive == false){
						isAll = false;
						return;
					}
				});
				this.isChooseAll = isAll;
			},
			chooseAll(){
				if(this.isChooseAll){
					this.isChooseAll = false;
					this.guessList.map(item=>{
						item.isActive = false;
					})
				}else{
					this.isChooseAll = true;
					this.guessList.map(item=>{
						item.isActive = true;
					})
				}
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	.guess {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items:center;
		padding:30upx 40upx 10upx;
	}
	.guess-list {
		margin:0 auto;
		// display: flex;
		// flex-wrap: wrap;
		width:670upx;
		height:160upx;
	}
	.guess-item {
		display: flex;
		width:100%;
		padding-bottom: 40upx;
	
		.image-wrapper{
			width: 160upx;
			height: 160upx;
			border-radius: 10upx;
		}
		.guess-content{
			height:160upx;
			width:420upx;
			span,text{
				display: block;
			}
		}
	}
	.fixed-buttons{
		
	}
	.button-group{
		width:670upx;
		display:flex;
		justify-content:space-between;
		.check{
			display:flex;
			align-items:center;
			image{
				margin-right:16upx;
				width:32upx;
				height:32upx;
			}
			span{
				color: #999999;
				font-size: 24upx;
			}
		}
		.finish{
			display: flex;
			align-items: center;
			.price{
				display: flex;
				margin-right:24upx;
				flex-direction: column;
				align-content: center;
				align-items: flex-end;
				span{
					line-height:32upx;
					display: inline-block;
				}
			}
		}
	}
		
</style>
