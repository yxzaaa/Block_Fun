<script>
	/**
	 * vuex管理登陆状态，具体可以参考官方登陆模板示例
	 */
	import {
		mapMutations
	} from 'vuex';
	export default {
		methods: {
			...mapMutations(['login'])
		},
		onLaunch: function() {
			let userInfo = uni.getStorageSync('userInfo') || '';
			if(userInfo){
				// 更新登陆状态
				// uni.getStorage({
				// 	key: 'userInfo',
				// 	success: (res) => {
				// 		this.login(res);
				// 	}
				// });
			}else{
				uni.reLaunch({
					url:'/pages/login/login'
				})
			}
			
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
	}
</script>

<style lang='scss'>
	/*
		全局公共样式和字体图标
	*/
	@import url('./static/fonts/montserrat.css');
   
	@font-face {
		font-family: yticon;
		font-weight: normal;
		font-style: normal;
		src: url('https://at.alicdn.com/t/font_1078604_w4kpxh0rafi.ttf') format('truetype');
	}
	
	@font-face {
		font-family: 'PingFang';
		src: url('./static/fonts/PingFang.ttf') format('truetype');  
	}

	.yticon {
		font-family: "yticon" !important;
		font-size: 16px;
		font-style: normal;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	.icon-yiguoqi1:before {
		content: "\e700";
	}

	.icon-iconfontshanchu1:before {
		content: "\e619";
	}

	.icon-iconfontweixin:before {
		content: "\e611";
	}

	.icon-alipay:before {
		content: "\e636";
	}

	.icon-shang:before {
		content: "\e624";
	}

	.icon-shouye:before {
		content: "\e626";
	}

	.icon-shanchu4:before {
		content: "\e622";
	}

	.icon-xiaoxi:before {
		content: "\e618";
	}

	.icon-jiantour-copy:before {
		content: "\e600";
	}

	.icon-fenxiang2:before {
		content: "\e61e";
	}

	.icon-pingjia:before {
		content: "\e67b";
	}

	.icon-daifukuan:before {
		content: "\e68f";
	}

	.icon-pinglun-copy:before {
		content: "\e612";
	}

	.icon-dianhua-copy:before {
		content: "\e621";
	}

	.icon-shoucang:before {
		content: "\e645";
	}

	.icon-xuanzhong2:before {
		content: "\e62f";
	}

	.icon-gouwuche_:before {
		content: "\e630";
	}

	.icon-icon-test:before {
		content: "\e60c";
	}

	.icon-icon-test1:before {
		content: "\e632";
	}

	.icon-bianji:before {
		content: "\e646";
	}

	.icon-jiazailoading-A:before {
		content: "\e8fc";
	}

	.icon-zuoshang:before {
		content: "\e613";
	}

	.icon-jia2:before {
		content: "\e60a";
	}

	.icon-huifu:before {
		content: "\e68b";
	}

	.icon-sousuo:before {
		content: "\e7ce";
	}

	.icon-arrow-fine-up:before {
		content: "\e601";
	}

	.icon-hot:before {
		content: "\e60e";
	}

	.icon-lishijilu:before {
		content: "\e6b9";
	}

	.icon-zhengxinchaxun-zhifubaoceping-:before {
		content: "\e616";
	}

	.icon-naozhong:before {
		content: "\e64a";
	}

	.icon-xiatubiao--copy:before {
		content: "\e608";
	}

	.icon-shoucang_xuanzhongzhuangtai:before {
		content: "\e6a9";
	}

	.icon-jia1:before {
		content: "\e61c";
	}

	.icon-bangzhu1:before {
		content: "\e63d";
	}

	.icon-arrow-left-bottom:before {
		content: "\e602";
	}

	.icon-arrow-right-bottom:before {
		content: "\e603";
	}

	.icon-arrow-left-top:before {
		content: "\e604";
	}

	.icon-icon--:before {
		content: "\e744";
	}

	.icon-zuojiantou-up:before {
		content: "\e605";
	}

	.icon-xia:before {
		content: "\e62d";
	}

	.icon--jianhao:before {
		content: "\e60b";
	}

	.icon-weixinzhifu:before {
		content: "\e61a";
	}

	.icon-comment:before {
		content: "\e64f";
	}

	.icon-weixin:before {
		content: "\e61f";
	}

	.icon-fenlei1:before {
		content: "\e620";
	}

	.icon-erjiye-yucunkuan:before {
		content: "\e623";
	}

	.icon-Group-:before {
		content: "\e688";
	}

	.icon-you:before {
		content: "\e606";
	}

	.icon-forward:before {
		content: "\e607";
	}

	.icon-tuijian:before {
		content: "\e610";
	}

	.icon-bangzhu:before {
		content: "\e679";
	}

	.icon-share:before {
		content: "\e656";
	}

	.icon-yiguoqi:before {
		content: "\e997";
	}

	.icon-shezhi1:before {
		content: "\e61d";
	}

	.icon-fork:before {
		content: "\e61b";
	}

	.icon-kafei:before {
		content: "\e66a";
	}

	.icon-iLinkapp-:before {
		content: "\e654";
	}

	.icon-saomiao:before {
		content: "\e60d";
	}

	.icon-shezhi:before {
		content: "\e60f";
	}

	.icon-shouhoutuikuan:before {
		content: "\e631";
	}

	.icon-gouwuche:before {
		content: "\e609";
	}

	.icon-dizhi:before {
		content: "\e614";
	}

	.icon-fenlei:before {
		content: "\e706";
	}

	.icon-xingxing:before {
		content: "\e70b";
	}

	.icon-tuandui:before {
		content: "\e633";
	}

	.icon-zuanshi:before {
		content: "\e615";
	}

	.icon-zuo:before {
		content: "\e63c";
	}

	.icon-shoucang2:before {
		content: "\e62e";
	}

	.icon-shouhuodizhi:before {
		content: "\e712";
	}

	.icon-yishouhuo:before {
		content: "\e71a";
	}

	.icon-dianzan-ash:before {
		content: "\e617";
	}

	.b-b:after, .b-t:after{
		border-bottom:none !important;
	}



	view,
	scroll-view,
	swiper,
	swiper-item,
	cover-view,
	cover-image,
	icon,
	text,
	rich-text,
	progress,
	button,
	checkbox,
	form,
	input,
	label,
	radio,
	slider,
	switch,
	textarea,
	navigator,
	audio,
	camera,
	image,
	video {
		box-sizing: border-box;
	}
	
	*{
		font-family: 'PingFang';
	}
	
	body{
		background-color:#15030B;
	}
	
	text span{
		font-family: inherit;
	}
	/* 骨架屏替代方案 */
	.Skeleton {
		background: rgba(255,255,255,0.1);
		border-radius: 8upx;
		margin-bottom:12upx;
		animation: flicker 1.6s infinite;
	}
	@keyframes flicker
	{
		0% {opacity:1;}
		50% {opacity:0.5;}
		100% {opacity:1;}
	}
	.clamp {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		display: block;
	}

	.common-hover {
		background: #f5f5f5;
	}

	/*边框*/
	.b-b:after,
	.b-t:after {
		position: absolute;
		z-index: 3;
		left: 0;
		right: 0;
		height: 0;
		content: '';
		transform: scaleY(.5);
		border-bottom: 1px solid $border-color-base;
	}

	.b-b:after {
		bottom: 0;
	}

	.b-t:after {
		top: 0;
	}

	/* button样式改写 */
	uni-button,
	button {
		height: 80upx;
		line-height: 80upx;
		font-size: $font-lg + 2upx;
		font-weight: normal;

		&.no-border:before,
		&.no-border:after {
			border: 0;
		}
	}

	uni-button[type=default],
	button[type=default] {
		color: $font-color-dark;
	}

	/* input 样式 */
	.input-placeholder {
		color: #999999;
	}

	.placeholder {
		color: #999999;
	}
	.container{
		position: relative;
	}
	.app-container{
		&.full{
			padding-top:194upx;
		}
		&.fixbutton{
			padding-bottom:120upx;
		}
	}
	.main-title{
		font-size: 32upx;
		color:#fff;
		text-align: center;
		padding:30upx 0upx;
	}
	.section-header{
		width:750upx;
		padding:40upx;
		padding-bottom:30upx;
		display:flex;
		justify-content:flex-start;
		align-items:center;
		.section-icon{
			width:40upx;
			height:40upx;
			margin-right:10upx;
		}
		.section-title{
			font-size: 32upx;
			color:#fff;
		}
	}
	.section-subtitle{
		font-size: 26upx;
		color:#fff;
		line-height: 54upx;
	}
	.section-describe{
		font-size: 26upx;
		color:#c7c7c7;
		line-height: 54upx;
	}
	.section-part{
		font-size: 26upx;
		color:#999;
		line-height: 54upx;
	}
	.section-content{
		padding:5px 40upx;
	}
	.button-group{
		display:flex;
		justify-content:space-between;
		.fun-btn{
			/* margin-left:20upx; */
		}
	}
	.fun-horizen{
		width:100%;
		height:2upx;
		background: rgba(255,255,255,.1);
	}
	.fun-card{
		width:670upx;
		background: rgba(45,31,37,0.7);
		border-radius: 8upx;
		overflow:hidden;
		position:relative;
		.fun-card-item{
			padding:40upx;
		}
		.item-horizen{
			display: flex;
			justify-content: flex-start;
			align-items: center;
		}
		.fun-card-buttons{
			width:100%;
			padding:20upx 0px;
			display: flex;
			justify-content: space-between;
		}
		.submit-btn{
			width:100%;
			height:100upx;
			line-height: 100upx;
			text-align: center;
			font-size:28upx;
			color:#DA53A2;
			background: rgba(218,83,162,0.2);
		}
	}
	.button-image{
		width:32upx;
		height:32upx;
		margin:30upx;
		display: block;
	}
	.fixed-buttons{
		position: fixed;
		bottom:0px;
		left:0px;
		width:750upx;
		padding:20upx 40upx;
		background: #2F282B;
		z-index:110;
		.certs{
			width:100%;
			display: flex;
			align-items: center;
			justify-content: center;
			padding:10upx 0;
			padding-top:30upx;
			.check-cert{
				width:24upx;
				height:24upx;
				margin-right:10upx;
			}
			.cert-text{
				color:#999;
				font-size:24upx;
				.cert-name{
					color:#DA53A2;
				}
			}
		}
	}
	.fun-table{
		width:100%;
		border-radius:20upx;
		overflow:hidden;
		.fun-table-header{
			width:100%;
			line-height: 74upx;
			text-align: center;
			background: #3A1F2D;
			color:#fff;
			font-size: 28upx;
			&.trans{
				background: transparent;
			}
		}
		.fun-table-body{
			width:100%;
			.fun-table-tr{
				width:100%;
				border-bottom:1px solid #45323B;
				display:flex;
				justify-content:space-between;
				overflow:hidden;
				&.noborder{
					border:none;
				}
				.trans{
					background:transparent;
					padding:15upx;
					line-height: 44upx;
					color:#999;
					text-align: center;
					font-size:26upx;
					&.white{
						color:#fff;
					}
					&.four{
						width:25%;
					}
					&.five{
						width:20%;
					}
					&.small{
						font-size:24upx;
					}
				}
				.deep{
					background: #281920;
					line-height: 74upx;
					color:#999;
					text-align: center;
					font-size:26upx;
					&.white{
						color:#fff;
					}
					&.four{
						width:25%;
					}
					&.five{
						width:20%;
					}
					&.small{
						font-size:24upx;
					}
				}
				.light{
					background: #311C26;
					line-height: 74upx;
					color:#999;
					text-align:center;
					font-size:26upx;
					&.white{
						color:#fff;
					}
					&.four{
						width:25%;
					}
					&.five{
						width:20%;
					}
					&.small{
						font-size:24upx;
					}
				}
			}
		}
	}
	
	.status-box{
		width:100%;
		display:flex;
		justify-content: space-between;
		.left-status{
			text{
				display: block;
				line-height: 52upx;
			}
		}
		.right-status{
			text-align:right;
			text{
				display: block;
				line-height: 52upx;
			}
		}
	}
	.check-box{
		border:1px solid rgba(255,255,255,0.5);
		border-radius: 18upx;
		width:96upx;
		height:36upx;
		overflow: hidden;
		display: flex;
		align-items: center;
		margin:0px;
		text{
			transition: all .3s;
			width:56upx;
			border-radius: 0px;
			height:26upx;
			border-radius:13upx;
			background:rgba(255,255,255,0.5);
			position:relative;
			transform:translateX(35upx);
			&.active{
				background:rgba(255,255,255,1);
				transform:translateX(4upx);
			}
		}
	}
	
	.form-item{
		width:100%;
		padding-bottom:20upx;
		.form-label{
			display: block;
			width:100%;
			font-size: 28upx;
			color:#fff;
			line-height: 40upx;
			.des-item{
				float:right;
				color:#999;
				font-size: 24upx;
			}
		}
		.form-value-box{
			padding-bottom:30upx;
			view{
				display: flex;
				align-items: center;
			}
		}
		.input-field{
			width:100%;
			border-radius: 6upx;
			background: #15030B;
			line-height: 72upx;
			padding:0upx 20upx;
			display:flex;
			justify-content:space-between;
			flex-wrap:wrap;
			.input-left{
				color:#999999;
			}
			.input-right{
				color:#999999;
			}
		}
		.form-input-box{
			padding-top:40upx;
			padding-bottom:20upx;
			display: flex;
			justify-content: space-between;
			border-bottom:1px solid rgba(255,255,255,.2);
			.form-input-field{
				width:calc(100% - 150upx);
				font-size: 26upx;
				color:#c7c7c7;
			}
			.form-input-btns{
				padding:0upx 20upx;
				width:150upx;
				display:flex;
				justify-content:flex-end;
				image{
					width:40upx;
					height:40upx;
					margin-left:15upx;
				}
				text{
					color:#DA53A2;
					font-size:26upx;
				}
			}
		}
	}
	.radio-box{
		width:100%;
		height:56upx;
		display:flex;
		justify-content:space-between;
		align-items: center;
		border-radius:8upx;
		margin-top:10upx;
		border:1px solid rgba(255,255,255,.5);
		position:relative;
		&.noborder{
			border:none;
		}
		text{
			line-height:56upx;
			display: block;
			color:#fff;
			font-size:26upx;
			text-align:center;
			border-radius:8upx;
			font-weight:bolder;
			&.active{
				background:#fff;
				color:#DA53A2;
			}
		}
	}
	@keyframes show{
		from {opacity: 0;}
		to {opacity: 1;}
	}
	.modal-box{
		opacity: 1;
		animation: show ease 0.3s 1;
		transition: all .5s;
		position: fixed;
		top:0px;
		left:0px;
		width:750upx;
		height:100vh;
		background: rgba(0,0,0,.5);
		z-index:120;
		display:flex;
		justify-content:center;
		align-items:center;
		.modal{
			width:560upx;
			border-radius: 12upx;
			background: #fff;
			overflow: hidden;
			.modal-top-item{
				width:100%;
				padding:20upx 40upx;
				.modal-title{
					width:100%;
					line-height: 64upx;
					font-size: 30upx;
					color:#000;
					padding-bottom:20upx;
					text-align: center;
					font-weight: bold;
				}
				.modal-content{
					width:100%;
					line-height: 48upx;
					font-size: 26upx;
					color:#000;
					.input-box{
						width:100%;
						display:flex;
						justify-content:center;
						align-items:center;
						
						input{
							display: block;
							width:300upx;
							height:64upx;
							line-height: 64upx;
							color:#DA53A2;
							background: #F2F8FF;
							text-align: center;
							font-weight: bold;
							font-size: 36upx;
							font-family:'Montserrat-Bold';
						}
					}
				}
			}
			.modal-btns{
				border-top:1px solid #eee;
				width:100%;
				display: flex;
				justify-content: space-between;
				view{
					width:50%;
					line-height: 100upx;
					height:100upx;
					color:#000;
					text-align: center;
					font-size: 32upx;
					&:active{
						background: #eee;
					}
				}
			}
		}
	}
	.swiper-box{
		width:750upx;
		height:calc(100vh - 250upx);
	}
	.fix-tabs-box{
		width:750upx;
		padding:0upx 40upx;
		display: flex;
		justify-content: space-between;
		border-bottom:1px solid rgba(255,255,255,0.2);
		position:relative;
		.fix-tabs-item{
			width:50%;
			line-height: 76upx;
			height:76upx;
			display:flex;
			justify-content:center;
			text{
				color:rgba(255,255,255,0.5);
				transition:all .4s;
				font-size:32upx;
				&.active{
					color:#fff;
					font-weight: bold;
					border-bottom:3upx solid #fff;
				}
			}
		}
	}
	/* page{
		background-image:url(static/bg.jpg);
		background-size:100% auto;
		background-repeat: no-repeat;
		background-color:#15030B;
	} */
	/* uni-page-body{
		background: transparent;
	}
	uni-page-head .uni-page-head{
		background-color: transparent;
	} */
</style>
