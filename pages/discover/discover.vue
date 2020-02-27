<template>
	<view class="content">
		<NavBar :tabTitle="tabTitle">
			<swiper-item v-for="(item,index) in contentTab" :key="index">
				<view :style="{backgroundColor: '#007AFF',height: '300px'}">
					{{item}}
				</view>
			</swiper-item>
		</NavBar>
		
		<view :animation="animationData" style="background:red;height:100rpx;width:100rpx"></view>
		
	</view>
</template>

<script>
	import NavBar from '../../components/navBar.vue'
	export default {
		data() {
			return {
				animationData: {},
				
				tabTitle: ["精选", "悬疑", "女性", "幻想", "文艺", "历史"],
				contentTab: ["内容1","内容2","33333333333","444444444","5555555555","66666666"]
			}
		},
		components:{
			NavBar
		},
		onShow: function(){
		    var animation = uni.createAnimation({
		      duration: 1000,
		      timingFunction: 'ease',
		    })

		
		    this.animation = animation
		
		    animation.width(150).height(150).rotate(360).step() 
		    // animation.scale(1,1).rotate(90).step()
		
		    this.animationData = animation.export()
		
		    // setTimeout(function() {
		    //   animation.translate(30).step()
		    //   this.animationData = animation.export()
		    // }.bind(this), 3000)
		  }
		  
	}
</script>

<style lang="less">

</style>
