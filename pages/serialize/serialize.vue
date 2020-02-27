<template>
	<view class="content" >
		<view style="width: 100%;">
			<scroll-view style="white-space: nowrap; display: flex;background-color: #FFFFFF;" :scroll-x="true" :scroll-left="tabLeft" scroll-with-animation>
				<view class="tabBar" :style='"width:"+isWidth+"px"' @click="tabBtn(index)" v-for="(item,index) in tabTitle" :key="item.index" :class="{active: index == num}">
					{{item}}
				</view>
				<view class="tabBox" :style='"transform:translateX("+isLeft+"px);width:"+isWidth+"px"'>
					<view class="tabBorder"></view>
				</view>
			</scroll-view>
			<view>
				<swiper :duration="duration" :current="num" @change="swiperTab">
					<swiper-item>
						<view :style="{backgroundColor: '#007AFF',height: '300px'}">
							内容1
						</view>
					</swiper-item>
					
					<swiper-item>
						<view>
							内容222222222222222
						</view>
					</swiper-item>
					
					<swiper-item>
						<view>
							内容3
						</view>
					</swiper-item>
					
					<swiper-item>
						<view>
							内容4
						</view>
					</swiper-item>
					
					<swiper-item>
						<view>
							内容5
						</view>
					</swiper-item>
					
					<swiper-item>
						<view>
							内容6
						</view>
					</swiper-item>
					
				</swiper>
			</view>
			<template>
			  <view class="content">
			    <chunLei-popups v-model="value" :popData="data" @tapPopup="tapPopup" :x="344" :y="0" placement="top-end">
			        </chunLei-popups>
			  </view>
			</template>
		</view>
	</view>
</template>

<script>
	import chunLeiPopups from "@/components/chunLei-popups/chunLei-popups.vue";
	export default {
		data () {
			return {
				value: false,
				data: [{title: '编辑'},{title: '分享'},{title: '收藏'}],
				
				// scrollLeft: 0,
				duration: 500,
				num: 0,
				tabTitle: ["精选", "悬疑", "女性", "幻想", "文艺", "历史"],
				contentTab: ["内容1","内容2","33333333333","444444444","5555555555","66666666"],
				
				tabClick: 0, //导航栏被点击
				isLeft: 0, //导航栏下划线位置
				isWidth: 0, //每个导航栏占位
				tabLeft:0
			}
		},
		components:{chunLeiPopups},
		created() {
			var that = this;
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
			tabBtn(index) {
				    if(this.tabTitle.length>5){
						var tempIndex = index - 2;
						tempIndex = tempIndex<=0 ? 0 : tempIndex;
						this.tabLeft = (index-2) * this.isWidth //设置下划线位置
					}
				this.num = index; //
				this.isLeft = index * this.isWidth //设置下划线位置
			},
			
			swiperTab(e) {
				var tabIndex = e.detail.current;
				this.tabBtn(tabIndex)
				// console.log(tabIndex)
			},
			tapPopup(item) {
				console.log(item)
				
			},
				
			 onNavigationBarButtonTap(value) {
				 if(value.type == "menu") {
					 if(this.value === false) {
					 	this.value = true
					 }else {
					 	this.value = false
					 }
			       console.log("菜单");  
				 }
			    }  
		}
	}
</script>

<style lang="less" scoped>
	.tabBar {
		// height: 90upx;
		line-height: 90rpx;
		color: #000;
		font-size: 12px;
		text-align: center;
		display: inline-block;
	}
	.tabBox {
		height: 3px;
		width: 20%;
		display: flex;
		align-content: center;
		justify-content: center;
		transition: .5s;
		.tabBorder {
			height: 4px;
			width: 120rpx;
			background-color: #1BD369;
		}
	}
	.active {
		// line-height: 50px;
		/* border-bottom: 2px solid #2C405A; */
	}
</style>
