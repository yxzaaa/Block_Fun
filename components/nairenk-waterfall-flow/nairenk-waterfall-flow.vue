<template>
	<view class="flow-box">
		<view class="item"
			:class="left[index] == 1 ? 'left' : ''"
			v-for="(item, index) in newList" :key="item.id"
			:data-index="index"
			 @click="choose(item.id)"
			 :style="{marginBottom:index==newList.length-1 || index==newList.length-2?'130upx':'',top:top[index]+'px'}"
			 >
			<view class="pic">
				<image class="image" mode="widthFix" :src="item.img" style="width: 100%; display: block;" ></image>
			</view>
			<view class="content">
				<view class="item-title" style="color:#fff;font-size:14px; margin-bottom:5px;">{{item.title}}</view>
				<view class="user">
					<text class="item-content">消耗积分</text>
					<text class="item-consume">{{item.credit}}</text>
				</view>
				<view>
					<text style="color:#DA53A2;font-size:28upx;margin-right:5upx;font-family:'Montserrat-Bold';">￥</text>
					<span style="color:#DA53A2;font-size:36upx;font-family:'Montserrat-Bold';">
						{{item.price.split('.')[0]}}
						<span style="font-size: 24upx;font-family:'Montserrat-Bold';">{{item.price.split('.')[1]?'.'+item.price.split('.')[1]:''}}</span>
					</span>
				</view>
			</view>
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
			}
		},
		data() {
			return {
				mark: 0,
				newList: [],
				boxHeight: [],
				top: [], 
				left: [],
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
						}
					}
				}).exec();
			},
			// 选中
			choose(id) {
				this.$emit('click', id);
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
		color: #999;
		.item-consume{
			color:#999;
		}
	}
	.loading {
		position: absolute;
		width: 100%;
		text-align: center;
		padding: 20upx 0;
	}
</style>
