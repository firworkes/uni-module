<template>
	<view class="content" >
		<view style="width: 100%;">
			<scroll-view style="white-space: nowrap; display: flex;background-color: #FFFFFF;" :scroll-x="true" :scroll-left="tabLeft" scroll-with-animation>
				<view :animation="animationData" class="tabBar" :style='"width:"+isWidth+"px"' @click="tabBtn(index)" v-for="(item,index) in tabTitle" :key="item.index" :class="{active: index == num}">
					{{item}}
				</view>
				<view class="tabBox" :style='"transform:translateX("+isLeft+"px);width:"+isWidth+"px"'>
					<view class="tabBorder" :style='"width:"+isWidth+"px"'></view>
				</view>
			</scroll-view>
			<view>
				<swiper :duration="duration" :current="num" @change="swiperTab">
					<slot></slot>
<!-- 					<swiper-item>
						<view :style="{backgroundColor: '#007AFF',height: '300px'}">
							
						</view>
					</swiper-item> -->
				</swiper>
			</view>
		</view>
	</view>
</template>

<script>

	export default {

		props:{
			tabTitle: {
				type: Array,
				default: []
			}
		},
		data () {
			return {
				duration: 500,
				num: 0,
				
				tabClick: 0, //导航栏被点击
				isLeft: 0, //导航栏下划线位置
				isWidth: 0, //每个导航栏占位
				tabLeft:0
			}
		},
		created() {
			var that = this;
			//获取设备宽度,得到tabTitle宽度
			uni.getSystemInfo({
				success(e) {
					if(that.tabTitle.length <= 5) {
						that.isWidth = e.windowWidth / that.tabTitle.length
					} else {
						that.isWidth = e.windowWidth / 5
					}
				}
			}) 
			
		},
		
		methods: {
			//tabTitle点击事件
			tabBtn(index) {
				    if(this.tabTitle.length>5){
						var tempIndex = index - 2;
						tempIndex = tempIndex<=0 ? 0 : tempIndex;
						this.tabLeft = (index-2) * this.isWidth //设置下划线位置
					}
				this.num = index; //点击对应标题
				this.isLeft = index * this.isWidth //设置下划线位置
				
			},
			
			//swiper滑动事件
			swiperTab(e) {
				var tabIndex = e.detail.current;
				this.tabBtn(tabIndex)
			},
		}
	}
</script>

<style lang="less" scoped>
	.tabBar {
		// height: 90upx;
		line-height: 90rpx;
		color: #555555;
		font-size: 12px;
		text-align: center;
		display: inline-block;
	}
	.active {
		color: #000;
		font-size: 16px;
	}

	.tabBox {
		height: 3px;
		display: flex;
		align-content: center;
		justify-content: center;
		transition: .5s;
		.tabBorder {
			height: 4px;
			// width: 120rpx;
			background-color: #ccc;
		}
	}

</style>
