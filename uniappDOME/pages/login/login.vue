<template>
   <view>
   
 <!--  	<view class="input-view">
   		<view class="texts"><input type="text" placeholder="点击输入搜索装备" confirm-type="search" placeholder-style="color:#FFCCCC;" /></view>
   		<view class="texts1">
   			<image src="../../static/sou.png"></image>
   		</view>
   	</view>
   -->
   	<view class="itess"> 
   		<view v-for="(item,index) in yx" class="image-view" :data-id="item.hero_id" @click="dianji">
   			<view>
   				<image class="uni-product-image" :src="item.icon"></image>
   				<view class="name">{{item.name}}</view>
				<view class="name">${{item.price}}</view>
   			</view>
   		</view>
   	</view>
   
   </view>
</template>

<script>
    export default {
        data() {
            return {
                 yx: [],
				search: "",
            }
        },
		onLoad() {
			this.diao();
		},
		onShow() {
			this.diao();
		},
		//下拉
		onPullDownRefresh() { 
			this.diao();
			uni.showToast({
				title: '加载中',
				duration: 1000,
				icon: 'loading'
			});
		},
        methods: {
    diao(){
		uni.request({
			url: 'http://gamehelper.gm825.com/wzry/equip/list?channel_id=90009a&app_id=h9044j&game_id=7622&game_name=%E7%8E%8B%E8%80%85%E8%8D%A3%E8%80%80&vcode=12.0.3&version_code=1203&cuid=2654CC14D2D3894DBF5808264AE2DAD7&ovr=6.0.1&device=Xiaomi_MI+5&net_type=1&client_id=1Yfyt44QSqu7PcVdDduBYQ%3D%3D&info_ms=fBzJ%2BCu4ZDAtl4CyHuZ%2FJQ%3D%3D&info_ma=XshbgIgi0V1HxXTqixI%2BKbgXtNtOP0%2Fn1WZtMWRWj5o%3D&mno=0&info_la=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&info_ci=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&mcc=0&clientversion=&bssid=VY%2BeiuZRJ%2FwaXmoLLVUrMODX1ZTf%2F2dzsWn2AOEM0I4%3D&os_level=23&os_id=dc451556fc0eeadb&resolution=1080_1920&dpi=480&client_ip=192.168.0.198&pdunid=a83d20d8',
			success: (res) => {
				
				this.yx = res.data.list;
				console.log("---------" + this.yx);
			}
		});
	}
        }
    }
</script>

<style>
	/* 	*{
		background: url(//game.gtimg.cn/images/yxzj/web201605/page/ny_con_bg.jpg)
	} */
	page {
		/* background:rgba(85, 85, 85, 0.01);  */
	}

	.input-view {
		width: 70%;
		border: 1px solid rgba(255, 192, 203);
		border-radius: 10px;
		margin-left: auto;
		margin-right: auto;
		display: flex;
		justify-content: center;
		height: 25px;
		/* 	-webkit-box-shadow:0px 3px 3px #c8c8c8 ;
		-moz-box-shadow:0px 3px 3px #c8c8c8 ;
		box-shadow:0px 3px 3px #c8c8c8 ; */
		/* box-shadow: 0 8px 8px rgba(10, 16, 20, .24), 0 0 8px rgba(255,192,203); */
		box-shadow: 0rpx 10rpx 50rpx 10rpx rgba(85, 85, 85, 0.1);
		text-decoration: none;
		margin-top: 3%;
		/* background-color:whitesmoke; */

	}

	.texts {
		width: 70%;
		height: 25px;
	}

	.texts1 {
		width: 20%;
		height: 25px;

		display: flex;
		justify-content: center;
		align-items: center;
	}

	.texts1 image {
		width: 20px;
		height: 20px;
		display: block;
	}

	.itess {
		margin-top: 3%;
		width: 95%;
		height: auto;
		margin-left: auto;
		margin-right: auto;
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
		/* background: url(//game.gtimg.cn/images/yxzj/web201605/page/ny_con_bg.jpg) */
		/* background-color: #99CC99; */
		/* box-shadow: 0 8px 8px rgba(10, 16, 20, .24), 0 0 8px rgba(255,192,203); */
		/* border: 1px solid  rgba(85, 85, 85); */
		/* box-shadow: 0rpx 10rpx 50rpx 10rpx rgba(85, 85, 85, 0.30); */
	}

	.image-view {
		border: 1px solid #FFCCCC;
		/* box-shadow: 0rpx 10rpx 50rpx 10rpx rgba(255,204,204, 0.15); */
		/* border: 1px solid #007AFF; */
		margin: 1%;
		width: 50px;
		border-radius: 10px 10px 10px 10px;
		background-color: #FFCCCC;
	}

	.uni-product-image {
		width: 50px;
		height: 50px;
		/* border: 1px solid rgba(255,204,204); 
		border-radius: 0px 10px 0px 10px; */
		border-radius: 10px 0px 10px 0px;
	}

	.name {
		/* border: 1px solid #007AFF; */
		text-align: center;
		color: #FFFFFF;
  font-size: 10px;
	}
</style>