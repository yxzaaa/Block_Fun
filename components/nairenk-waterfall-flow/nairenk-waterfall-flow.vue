<template>
	<view class="flow-box" style="">
		<view class="item"
			:class="left[index] == 1 ? 'left' : ''"
			v-for="(item, index) in newList" :key="index"
			:data-index="index"
			 @click="choose"
			 :style="{marginBottom:index==newList.length-1 || index==newList.length-2?'130upx':'',top:top[index]+'px'}"
			 >
			<view class="pic">
				<image class="image" mode="widthFix" :src="item.image" style="width: 100%; display: block;" ></image>
			</view>
			<view class="content">
				<view class="item-title" style="color:#fff;font-size:14px; margin-bottom:5px;">{{item.title}}</view>
				<view class="user">
					<text class="item-content">{{item.content}}</text>
					<text class="item-consume">{{item.consume}}</text>
				</view>
				<view>
					<text style="color:#DA53A2;font-size:28upx;font-weight: bold;margin-right:5upx;">{{item.symbol}}</text>
					<text style="color:#DA53A2;font-size:36upx;font-weight: bold">
						{{item.money.split('.')[0]}}
						<span style="font-size: 24upx;">{{item.money.split('.')[1]?'.'+item.money.split('.')[1]:''}}</span>
					</text>
				</view>
			</view>
		</view>
		<view class="loading" v-show="loading" :style="'top: ' + loadingTop + 'px'" >
			<image src="/static/nairenk-waterfall-flow/loading.gif" style="width: 80upx; height: 80upx;"></image>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			// 数据列表
			list: {
				type: Array,
				default() {
					return []
				}
			},
			// 加载动画
			loading: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				mark: 0,
				newList: [],
				boxHeight: [],
				top: [], 
				left: [],
				loadingTop: 0
			}
		},
		watch: {
			// 数据
			list: function (newVal, oldVal) {
				this.mark = oldVal.length;
				if (newVal != oldVal) {
					this.newList = this.list;
					console.log(this.newList)
					this.$nextTick(function () {
						setTimeout(() => {
							this.waterFall();
						}, 120)
					})
				}
			}
		},
		mounted(){

			this.newList = this.list;
			this.$nextTick(function () {
				setTimeout(() => {
					this.waterFall();
				}, 120)
			})
		},
		methods: {
			// 瀑布流定位
			waterFall() {
				const query = uni.createSelectorQuery().in(this);
				query.selectAll('.flow-box .item').boundingClientRect(res => {
					let len = this.newList.length;
					let height = 0;
					for (let i = this.mark; i < len; i++) {
						height = res[i].height;
						if (i < 2) {
							this.$set(this.newList[i], 'top', 0);
							this.$set(this.newList[i], 'left', i);
							this.boxHeight.push(height);
							this.top.push(0);
							this.left.push(i);
						} else {
							let minHeight = this.boxHeight[0];
							let index = 0;
							if (minHeight > this.boxHeight[1]) {
								minHeight = this.boxHeight[1];
								index = 1;
							}
							this.boxHeight[index] = minHeight + height + 10;
							this.top.push(minHeight + 10);
							this.left.push(index);
							this.$set(this.newList[i], 'top', minHeight + 10);
							this.$set(this.newList[i], 'left', index);
							this.loadingTop = this.boxHeight[index];
						}
					}
				}).exec();
			},
			// 选中
			choose(e) {
				let index = e.currentTarget.dataset.index;
				this.$emit('click', this.newList[index]);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.flow-box {
		position: relative;
		padding-bottom:20px;		
	}
	.flow-box .item {
		position: absolute;
		left: 40upx;
		width: calc(50% - 50upx);
		border-radius: 8upx;
		overflow: hidden;
		
			
			
	}
	.flow-box .left {
		left: 390upx;
	}
	.flow-box .pic {
		background: #f6f6f6;
	}
	.flow-box .content {
		padding: 20upx;
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
		background:#281920;
		
	}
	.flow-box .content text {
		width: 100%;
		font-size: 24upx;
		margin-bottom: 20upx;
	}
	.flow-box .user {
		display: flex;
		width: 220upx;
		overflow: hidden;
		font-size: 26upx;
		color: #666;
		.item-consume{
			color:#fff
		}
	}
	.loading {
		position: absolute;
		width: 100%;
		text-align: center;
		padding: 20upx 0;
	}
</style>
