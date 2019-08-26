<template>
	<view class="nav-bar-box" :style="{justifyContent:layout=='left'?'flex-start':'center'}">
		<view v-show="layout == 'left'" class="left-box">
			<view class="left-title">{{title}}</view>
			<view class="left-subtitle">{{subTitle}}</view>
		</view>
		<view class="center-box" v-show="layout == 'center'">
			<text
				class="nav-bar-title" 
				:style="{color:textColor}"
			>
				{{title}}
			</text>
		</view>
		<view class="search-bar-box" v-show="layout=='search'">
			<div class="search-input-box">
				<input type="text" class="search-input" placeholder="请输入商品信息" :focus="searchFocus">
				<image src="../../static/icons/input-search.png" class="input-icon" />
			</div>
		</view>
		<view class="search-bar-box" v-show="layout=='searchbtn'">
			<div class="search-input-box" @click="navigatorBack({text:'搜索',url:'../search/search'})">
				<input type="text" class="search-input" placeholder="请输入商品信息" disabled>
				<image src="../../static/icons/input-search.png" class="input-icon" />
			</div>
		</view>
		<view
			:class="['back-btn','icon-box',buttons && buttons.back && buttons.back.type=='circle'?'circle':'']" 
			v-show="buttons && buttons.back"
			@click="navigatorBack(buttons && buttons.back)"
			:style="{backgroundColor:buttons && buttons.back && buttons.back.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
		>
			<image class="icon-img" src="../../static/icons/back.png" />
		</view>
		<view class="right-btn-list">
			<view 
				:class="['icon-box',buttons && buttons.share && buttons.share.type=='circle'?'circle':'']" 
				v-show="buttons && buttons.share"
				:style="{backgroundColor:buttons && buttons.share && buttons.share.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<image class="icon-img" src="../../static/icons/share.png" />
			</view>
			<view
				:class="['icon-box',buttons && buttons.love && buttons.love.type=='circle'?'circle':'']" 
				v-show="buttons && buttons.love"
				:style="{backgroundColor:buttons && buttons.love && buttons.love.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<image class="icon-img" src="../../static/icons/love.png" />
			</view>
			<view 
				:class="['cart-btn','icon-box',buttons && buttons.cart && buttons.cart.type=='circle'?'circle':'']" 
				v-show="buttons && buttons.cart"
				:style="{backgroundColor:buttons && buttons.cart && buttons.cart.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
				@click="navigatorBack(buttons && buttons.cart)"
			>
					<image class="icon-img" src="../../static/icons/cart.png" />	
			</view>
			<view
				:class="['icon-box',buttons && buttons.search && buttons.search.type=='circle'?'circle':'']" 
				v-show="buttons && buttons.search"
				:style="{backgroundColor:buttons && buttons.search && buttons.search.type=='circle'?'rgba(0,0,0,'+(backOpacity-priviteOpacity)+')':'transparent'}"
			>
				<image class="icon-img" src="../../static/icons/search.png" />
			</view>
			<view
				class="icon-text-box" 
				v-show="buttons && buttons.textbtn"
			>
				<text class="text-btn" @click="navigatorBack(buttons && buttons.textbtn)">{{buttons && buttons.textbtn && buttons.textbtn.text}}</text>
			</view>
		</view>
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
				this.priviteOpacity = (val/200).toFixed(2);
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
				}else{
					uni.navigateTo({
						url:obj.url
					})
				}
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
		padding-top:28px;
		height:72px;
		z-index:10000;
		display:flex;
		align-items:center;
		.back-btn{
			position:absolute;
			bottom:4px;
			left:24upx;
		}
		.right-btn-list{
			position:absolute;
			bottom:4px;
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
			padding:0upx 30upx;
			.left-title{
				color:#fff;
				font-size: 18px;
				font-weight: bold;
			}
			.left-subtitle{
				color:#fff;
				font-size: 10px;
				padding-left:5upx;
			}
		}
		.center-box{
			
		}
		.search-bar-box{
			width:100%;
			padding:2px 30upx;
			display:flex;
			justify-content:space-between;
			.search-input-box{
				position:relative;
				width:596upx;
				height:40px;
				.search-input{
					width:100%;
					height:100%;
					padding:0px 30upx;
					background: #15030B;
					color:#fff;
					opacity: 0.5;
					font-size: 15px;
					padding-right:80upx;
				}
				.input-icon{
					position: absolute;
					width:30px;
					height:30px;
					top:5px;
					right:5px;
				}
			}
			.leave-search{
				color:#fff;
				font-size: 16px;
				width:100upx;
				line-height: 40px;
			}
		}
		.icon-box{
			width:36px;
			height:36px;
			border-radius:18px;
			text-align:center;
			.icon-img{
				width:36px;
				height:36px;
				display: inline-block;
			}
		}
		.icon-text-box{
			height:36px;
			padding:0px 5px;
			.text-btn{
				line-height:36px;
				color:#DA53A2;
				font-size: 30upx;
			}
		}
		.icon-box.circle{
			background: rgba(0,0,0,.2);
		}
	}
</style>
