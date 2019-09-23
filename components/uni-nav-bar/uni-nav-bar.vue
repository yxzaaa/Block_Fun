<template>
	<view class="nav-bar-box" :style="{justifyContent:layout=='left'?'flex-start':'center',position:opacity == 0?'absolute':'fixed'}">
		<!-- 左侧布局标题，副标题 -->
		<view v-if="layout === 'left'" class="left-box">
			<view class="left-title">{{title}}</view>
			<view class="left-subtitle">{{subTitle}}</view>
		</view>
		<!-- 居中布局标题 -->
		<view class="center-box" v-if="layout === 'center'">
			<text
				class="nav-bar-title" 
				:style="{color:textColor}"
			>
				{{title}}
			</text>
		</view>
		<!-- 搜索框布局 -->
		<view class="search-bar-box" v-if="layout === 'search'">
			<div class="search-input-box">
				<input @input="input" type="text" class="search-input" placeholder="请输入商品信息" :focus="searchFocus">
				<image src="../../static/icons/input-search.png" class="input-icon" @click="search"/>
			</div>
		</view>
		<!-- 搜索按钮布局，与搜索框配套存在 -->
		<view class="search-bar-box" v-if="layout === 'searchbtn'">
			<div class="search-input-box" @click="navigatorBack({text:'搜索',url:'../search/search'})">
				<input type="text" class="search-input" placeholder="请输入商品信息" disabled>
				<image src="../../static/icons/input-search.png" class="input-icon" />
			</div>
		</view>
		<!-- 路由返回按钮 -->
		<view
			:class="['back-btn','icon-box',buttons && buttons.back && buttons.back.type=='circle'?'circle':'']" 
			v-if="buttons && buttons.back"
			@click="navigatorBack(buttons && buttons.back)"
			:style="{backgroundColor:buttons && buttons.back && buttons.back.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
		>
			<image class="icon-img" src="../../static/icons/back.png" />
		</view>
		<!-- 右侧按钮组布局 -->
		<view class="right-btn-list">
			<!-- 设置图标 -->
			<view
				@click="navigatorBack(buttons && buttons.setting)"
				:class="['icon-box',buttons && buttons.setting && buttons.setting.type=='circle'?'circle':'']" 
				v-if="buttons && buttons.setting"
				:style="{backgroundColor:buttons && buttons.setting && buttons.setting.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<image class="icon-img" src="../../static/icons/icon_settings.png" />
			</view>
			<!-- 分享图标 -->
			<view 
				@click="navigatorBack(buttons && buttons.share)"
				:class="['icon-box',buttons && buttons.share && buttons.share.type=='circle'?'circle':'']" 
				v-if="buttons && buttons.share"
				:style="{backgroundColor:buttons && buttons.share && buttons.share.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<image class="icon-img" src="../../static/icons/share.png" />
			</view>
			<!-- 收藏图标 -->
			<view
				@click="navigatorBack(buttons && buttons.love)"
				:class="['icon-box',buttons && buttons.love && buttons.love.type=='circle'?'circle':'']" 
				v-if="buttons && buttons.love"
				:style="{backgroundColor:buttons && buttons.love && buttons.love.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<!-- 未激活状态 -->
				<image v-if="buttons && buttons.love && !buttons.love.active" class="icon-img" src="../../static/icons/love.png" />
				<!-- 激活状态 -->
				<image v-if="buttons && buttons.love && buttons.love.active" class="icon-img" src="../../static/icons/love-active.png" />
			</view>
			<!-- 购物车图标 -->
			<view 
				@click="navigatorBack(buttons && buttons.cart)"
				:class="['icon-box',buttons && buttons.cart && buttons.cart.type=='circle'?'circle':'']" 
				v-if="buttons && buttons.cart"
				:style="{backgroundColor:buttons && buttons.cart && buttons.cart.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<!-- 未激活状态 -->
				<image v-if="buttons && buttons.cart && !buttons.cart.active" class="icon-img" src="../../static/icons/cart.png" />	
				<!-- 激活状态 -->
				<image v-if="buttons && buttons.cart && buttons.cart.active" class="icon-img" src="../../static/icons/cart-active.png" />
			</view>
			<!-- 搜索图标 -->
			<view
				@click="navigatorBack(buttons && buttons.search)"
				:class="['icon-box',buttons && buttons.search && buttons.search.type=='circle'?'circle':'']" 
				v-if="buttons && buttons.search"
				:style="{backgroundColor:buttons && buttons.search && buttons.search.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<image class="icon-img" src="../../static/icons/search.png" />
			</view>
			<!-- 纯文本按钮 -->
			<view
				class="icon-text-box" 
				v-if="buttons && buttons.textbtn"
			>
				<text class="text-btn" @click="navigatorBack(buttons && buttons.textbtn)">{{buttons && buttons.textbtn && buttons.textbtn.text}}</text>
			</view>
		</view>
		<!-- 背景块 -->
		<view class="nav-bg-block" :style="{opacity:priviteOpacity}"></view>
	</view>
</template>

<script>
	export default{
		props:{
			title:{
				type:String,
				default:''
			},
			subTitle:{
				type:String,
				default:'Unblockgrace'
			},
			textColor:{
				type:String,
				default:'#000000'
			},
			layout:{
				type:String,
				default:'center'
			},
			opacity:{
				type:Number,
				default:0
			},
			buttons:{
				type:Object
			}
		},
		data(){
			return {
				priviteOpacity:0,
				backOpacity:0.5,
				searchFocus:false
			}
		},
		watch:{
			opacity(val){
				this.priviteOpacity = (val/120).toFixed(2);
			}
		},
		mounted(){
			if(this.layout == 'search'){
				this.searchFocus = true;
			}
		},
		methods:{
			navigatorBack(obj){
				if(obj.text === '取消'){
					uni.navigateBack({
						delta:1
					})
				}else if(obj.text === 'handle' || obj.type === 'handle'){
					this.$emit('handle',obj.classify)
				}else{
					uni.navigateTo({
						url:obj.url
					})
				}
			},
			input(e){
				this.$emit('input',e.detail.value);
			},
			search(){
				this.$emit('search');
			}
		}
	}
</script>

<style lang="scss" scoped>
	.nav-bar-box{
		position: fixed;
		top:0;
		left:0;
		width:100%;
		padding-top:66upx;
		height:164upx;
		z-index:100;
		display:flex;
		align-items:center;
		transition:all 1s;
		.back-btn{
			position:absolute;
			bottom:14upx;
			left:24upx;
		}
		.right-btn-list{
			position:absolute;
			bottom:14upx;
			right:30upx;
			display:flex;
			justify-content:flex-end;
			align-items:center;
			.icon-box{
				margin-left:5px;
			}
		}
		.nav-bg-block{
			position: absolute;
			top:0;
			left:0;
			width:100%;
			height:100%;
			z-index:-1;
			background-image:url(../../static/bg.jpg);
			background-size:100% auto;
			background-repeat: no-repeat;
			background-color:#15030B;
			overflow: hidden;
		}
		.left-box{
			padding:0upx 40upx;
			.left-title{
				color:#fff;
				font-size: 36upx;
				font-family:'Montserrat-Bold';
			}
			.left-subtitle{
				color:#c7c7c7;
				font-size: 20upx;
				padding-left:5upx;
				font-family:'Montserrat-Light';
			}
		}
		.center-box{
			.nav-bar-title{
				font-size:34upx;
			}
		}
		.search-bar-box{
			width:100%;
			padding:4upx 30upx;
			display:flex;
			justify-content:space-between;
			.search-input-box{
				position:relative;
				width:596upx;
				height:80upx;
				.search-input{
					width:100%;
					height:100%;
					padding:0px 30upx;
					background: #15030B;
					color:#fff;
					opacity: 0.5;
					font-size: 30upx;
					padding-right:80upx;
				}
				.input-icon{
					position: absolute;
					width:60upx;
					height:60upx;
					top:10upx;
					right:10upx;
				}
			}
			.leave-search{
				color:#fff;
				font-size: 32upx;
				width:100upx;
				line-height: 80upx;
			}
		}
		.icon-box{
			width:72upx;
			height:72upx;
			border-radius:36upx;
			text-align:center;
			.icon-img{
				width:72upx;
				height:72upx;
				display: inline-block;
			}
		}
		.icon-text-box{
			height:72upx;
			padding:0px 10upx;
			.text-btn{
				line-height:72upx;
				color:#DA53A2;
				font-size: 28upx;
			}
		}
		.icon-box.circle{
			background: rgba(0,0,0,.2);
		}
	}
</style>
