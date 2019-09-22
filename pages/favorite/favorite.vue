<template>
	<view class="container">	
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
						v-for="(item, index) in favoriteList" :key="index"
						class="guess-item"		
					>
					<!-- 引入图片 -->
						<view style="line-height: 160upx;padding-right:30upx;" v-show="isManager" @click="itemChoose(index,item.id)">
							<image
								:src="item.isActive?imageLib.checked:imageLib.check"
								style="width:40upx;height:40upx;"
							></image>
						</view>
						<view @click="showDetail(item.id)" :style="{marginTop:'0',width:isManager?'610upx':'690upx',display:'flex',justifyContent:'flex-start'}">
							<view class="image-wrapper">
								<image 
									:src="item.img" 
									mode="aspectFill"
									style="width:160upx;height:160upx;"
								></image>
							</view>
							<!-- 图片描述 -->
							<view class="guess-content" :style="{marginLeft:'20upx',marginTop:'0',width:isManager?'420upx':'490upx'}">
								<span style="font-size: 28upx;color:#fff;height:80upx;">{{item.title.length>36?item.title.substring(0,36)+' ...':item.title}}</span>
								<text style="font-size:24upx;color:#999999;margin-top:4upx;">消耗积分 {{item.credit}}</text>
								<span style="color:#DA53A2;">
									<span style="font-size:24upx;margin-right:8upx;display: inline-block;font-family:'Montserrat-Bold';">￥</span>
									<span style="display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[0]}}</span>
									<span style="font-size:24upx;display: inline-block;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
								</span>
							</view>
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
					<fun-button value="删除" width="240upx" @handle="deleteFav" large></fun-button>
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
				favoriteList:[],
				ids:new Set(),
				isManager:false,
				isChooseAll:false,
			};
		},
		onPageScroll(val){
			this.scroll = val.scrollTop;
		},
		onLoad(){
			this.updateList();
		},
		methods:{
			updateList(){
				this.$http({
					url:'/member/favorite',
					success:res=>{
						console.log(res);
						if(res.code == 200){
							this.favoriteList = res.data;
							this.favoriteList.map(item=>{
								item.isActive = false;
							})
						}
					}
				})
			},
			showDetail(id){
				uni.navigateTo({
					url:"../detail/detail?id="+id
				})
			},
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
			itemChoose(index,id){
				console.log(index,id);
				if(this.favoriteList[index].isActive === true){
					// this.favoriteList[index].isActive = false;
					this.$set(this.favoriteList[index],'isActive',false);
					this.ids.delete(id);
				}else{
					// this.favoriteList[index].isActive = true;
					this.$set(this.favoriteList[index],'isActive',true);
					this.ids.add(id);
				}
				var isAll = true;
				this.favoriteList.map(item=>{
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
					this.ids.clear();
					this.favoriteList.map(item=>{
						item.isActive = false;
					})
				}else{
					this.isChooseAll = true;
					this.favoriteList.map(item=>{
						this.ids.add(item.id);
						item.isActive = true;
					})
				}
			},
			deleteFav(){
				console.log(Array.from(this.ids));
				var arr = Array.from(this.ids);
				this.$http({
					url:'/member/favorite',
					type:'application/x-www-form-urlencoded',
					data:{
						action:'delete',
						id:arr.join(',')
					},
					success:res=>{
						console.log(res);
						if(res.code == 200){
							this.updateList();
						}
					}
				})
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
			border-radius: 8upx;
			overflow: hidden;
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
