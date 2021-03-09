<template>
	<view>
		<view>
			<view v-for="(itemzong,index) in textObj">
				<view>
				
					<view class="one">
							<image :src="xiandapifu" mode="scaleToFill" class="topimg"></image>
							<view class="one-yxzil">
						<view class="pifumz">
							{{xianmz}}
						</view>
						<view class="yxmz">{{itemzong.name}}</view>
						<view @click="yxzl()" class="yxziliao">英雄资料</view>
						</view>
						

					</view>
					
					<!-- <view v-if="yxzlbool">
						<view @click="guan">X</view>
						<view>{{itemzong.background_story}}</view>
					</view>
 -->
					<view class="two">
						<view class="pifuview">皮肤</view>
						<scroll-view scroll-x="true" scroll-top="0" scroll-left="0" > 	
											<view class="pifu">
						<view v-for="(pifu,indexpifu) in pifus" class="pifu-view" @click="pifuitem(indexpifu)"   :class="(indexpifu == pifuindex) ? 'pifudongclass':''">
							<view class="imgaview" >
								<image :src="pifu.big_img" class="pifuimg" ></image> 
							</view>
							<view class="pifu-name" :class="(indexpifu == pifuindex) ? 'pifudongclass':''">{{pifu.skin_name}}</view>
						</view>
							</view>
						</scroll-view >
					</view>

					<view class="there">
						<view class="jinengtext">技能介绍</view>
						<view class="jinenflex">
						<view v-for="(jinengs,indexjineng) in jineng" @click="jinengclick(indexjineng)" >
							<view class="jineng-img" :class="(indexjineng == jinengone) ? 'pifudongclass2':''">
								<image :src="jinengs.icon" class="pifuimg1" ></image>
							</view>
						</view>
						</view>
						<view class="jinengname">
							{{jineng[jinengone].name}}
						</view>
						<view v-for="(attrsts,indexattrs) in jineng[jinengone].attrs" class="shanghai"> 
							<view>{{attrsts}}</view>
						</view>
						<view class="jineng">
							{{jineng[jinengone].description}}
						</view>
						<!-- </view> -->
						<view class="duixianjiqiao">
													对线技巧:{{skill_tips}}
												</view>
						
					</view>



					<view class="si">
						<view class="sifuwendapei">
							符文搭配建议
						</view>
						<view>
							<view v-for="(rec_inscriptionst,indexrec_inscriptions) in rec_inscriptions">

								<view class="bian1">
									<view v-for="(fuwen,fuwenindex) in rec_inscriptionst.list" class="bian-view">
										<view>
											<image :src="fuwen.icon" class="pifuimg"></image>
										</view>
										<view class="fuwen-name"> {{fuwen.name}}</view>
										<view class="fuwen-shuxin">{{fuwen.attrs}}</view>
										
									</view>
								</view>
							</view>
						</view>
					</view>
					


					<view class="wu">
						<view class="chuzhuantj">
							出装推荐:
						</view>
						<view> 
						
						<view class="wuone">
							<view v-for="(equip_choicest,indexequip_choice) in equip_choice" class="wuone-item" :class="(indexequip_choice == chuzhuanindex) ? 'pifudongclass3':''">
								<view @click="chuzhuanclick(indexequip_choice)">{{equip_choicest.title}}</view>
                             </view>
							</view>
							
							<view >
								<view class="wu-for">
								<view v-for="(chuzhuan,indexchuzuan) in equip_choice[chuzhuanindex].list">
									<view>
										<image :src="chuzhuan.icon" class="pifuimg"></image>
									</view>
								</view>
								</view>
								<view class="witwo">{{description}}</view>
								
							</view>
						</view>
					</view>


					<view class="liu">
						<view class="yxguanxi">英雄关系</view>
						<view class="bianliu">
							<view class="nane-yxyx">最佳搭档</view>
							<view class="liu-there">
							<view v-for="(partner_herost,indexpartner_hero) in partner_hero"  class="liusi">
							
								<view>
									<image :src="partner_herost.icon" class="pifuimg" @click="zuijia(partner_herost.hero_id)"></image>
								</view>
									<view class="liu-text">{{partner_herost.name}}</view>
							</view>
							</view>
						</view>

						<view class="bianliu">
							<view class="nane-yxyx">压制英雄</view>
							<view class="liu-there">
							<view v-for="(restrained_herost,indexrestrained_hero) in restrained_hero" class="liusi">
						
								<view>
									<image :src="restrained_herost.icon" class="pifuimg" @click="yazhi(restrained_herost.hero_id)"></image>
								</view>
										<view class="liu-text">{{restrained_herost.name}}</view>
							</view>
							</view>
						</view>

						<view class="bianliu">
							<view class="nane-yxyx">被压制英雄</view>
							
							<view class="liu-there">
							<view v-for="(be_restrained_herost,indexbe_restrained_hero) in be_restrained_hero"  class="liusi">
								<view>
									<image :src="be_restrained_herost.icon" class="pifuimg" @click="beiyazhi(be_restrained_herost.hero_id)"></image>
								</view>
								<view class="liu-text">{{be_restrained_herost.name}}</view>
							</view>
							</view>
							
						</view>

					</view>


				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				textObj: [],
				yxzl1:'', 
				pifus: [], //皮肤
				xiandapifu: '',
				xianmz: '',
				pifuindex: 0,
				yxzlbool: false,
				jineng: [], //技能
				jinengone: 0,
				rec_inscriptions: [], //符文
				skill_tips: '',
				equip_choice: [], //出装
				chuzhuanindex: 0,
				description: '',
				be_restrained_hero: [],
				restrained_hero: [],
				partner_hero: []
			}
		},
		onLoad(options) {
			var textObj = JSON.parse(options.textObj);
			this.textObj.push(textObj);
			this.skill_tips = textObj.skill_tips;
			this.pifus = textObj.skin_imgs; //皮肤
			this.jineng = textObj.skill_list; //技能
			this.equip_choice = textObj.equip_choice; //出装
			
			this.yxzl1 = textObj.background_story; //背景故事
			// console.log(this.jineng);
			this.rec_inscriptions = textObj.rec_inscriptions; //符文
			// this.be_restrained_hero = textObj.be_restrained_hero;//被克制英雄
			this.be_restrained_hero = textObj.be_restrained_hero; //被克制英雄
			this.restrained_hero = textObj.restrained_hero; //限制英雄
			this.partner_hero = textObj.partner_hero; //搭档英雄
			this.xianmz = this.pifus[this.pifuindex].skin_name;
			this.xiandapifu = this.pifus[this.pifuindex].big_img;
			this.description = this.equip_choice[this.chuzhuanindex].description;
		},
		methods: {
			pifuitem(indexpifu) {
				console.log(indexpifu)
				this.pifuindex = indexpifu;
				this.xianmz = this.pifus[this.pifuindex].skin_name;
				this.xiandapifu = this.pifus[this.pifuindex].big_img;
			},
			yxzl() {
				// this.yxzl = true;
				console.log("dasdasd");
				// this.yxzlbool = !this.yxzlbool;
				uni.showModal({
					title:'英雄资料',
					content:this.yxzl1,
				    success: function (res) {
				        if (res.confirm) {
				            console.log('用户点击确定');
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
			},
			guan() {
				this.yxzlbool = false;
			},
			jinengclick(indexjineng) {

				this.jinengone = indexjineng;
				console.log(this.jinengone);
			},
			chuzhuanclick(indexequip_choice) {


				this.chuzhuanindex = indexequip_choice;
				this.description = this.equip_choice[this.chuzhuanindex].description;

			},
			zuijia(id) {
				// console.log(id);
				var hero_id = id;
				uni.request({
					url: 'http://gamehelper.gm825.com/wzry/hero/detail?hero_id=1&channel_id=90009a&app_id=h9044j&game_id=7622&game_name=%E7%8E%8B%E8%80%85%E8%8D%A3%E8%80%80&vcode=12.0.3&version_code=1203&cuid=2654CC14D2D3894DBF5808264AE2DAD7&ovr=6.0.1&device=Xiaomi_MI+5&net_type=1&client_id=1Yfyt44QSqu7PcVdDduBYQ%3D%3D&info_ms=fBzJ%2BCu4ZDAtl4CyHuZ%2FJQ%3D%3D&info_ma=XshbgIgi0V1HxXTqixI%2BKbgXtNtOP0%2Fn1WZtMWRWj5o%3D&mno=0&info_la=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&info_ci=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&mcc=0&clientversion=&bssid=VY%2BeiuZRJ%2FwaXmoLLVUrMODX1ZTf%2F2dzsWn2AOEM0I4%3D&os_level=23&os_id=dc451556fc0eeadb&resolution=1080_1920&dpi=480&client_ip=192.168.0.198&pdunid=a83d20d8',
					data: {
						hero_id: hero_id
					},
					success: (res) => {
						this.xq = res.data.info;
						console.log("---------" + this.xq);
						var textObj = JSON.stringify(this.xq);
						uni.reLaunch({
							url: "/pages/xingqin/xingqin?textObj=" + textObj
						});
					}
				});
			},
			yazhi(id) {
				var hero_id = id;
				uni.request({
					url: 'http://gamehelper.gm825.com/wzry/hero/detail?hero_id=1&channel_id=90009a&app_id=h9044j&game_id=7622&game_name=%E7%8E%8B%E8%80%85%E8%8D%A3%E8%80%80&vcode=12.0.3&version_code=1203&cuid=2654CC14D2D3894DBF5808264AE2DAD7&ovr=6.0.1&device=Xiaomi_MI+5&net_type=1&client_id=1Yfyt44QSqu7PcVdDduBYQ%3D%3D&info_ms=fBzJ%2BCu4ZDAtl4CyHuZ%2FJQ%3D%3D&info_ma=XshbgIgi0V1HxXTqixI%2BKbgXtNtOP0%2Fn1WZtMWRWj5o%3D&mno=0&info_la=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&info_ci=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&mcc=0&clientversion=&bssid=VY%2BeiuZRJ%2FwaXmoLLVUrMODX1ZTf%2F2dzsWn2AOEM0I4%3D&os_level=23&os_id=dc451556fc0eeadb&resolution=1080_1920&dpi=480&client_ip=192.168.0.198&pdunid=a83d20d8',
					data: {
						hero_id: hero_id
					},
					success: (res) => {
						this.xq = res.data.info;
						console.log("---------" + this.xq);
						var textObj = JSON.stringify(this.xq);
						uni.reLaunch({
							url: "/pages/xingqin/xingqin?textObj=" + textObj
						});
					}
				});

			},
			beiyazhi(id) {
				var hero_id = id;
				uni.request({
					url: 'http://gamehelper.gm825.com/wzry/hero/detail?hero_id=1&channel_id=90009a&app_id=h9044j&game_id=7622&game_name=%E7%8E%8B%E8%80%85%E8%8D%A3%E8%80%80&vcode=12.0.3&version_code=1203&cuid=2654CC14D2D3894DBF5808264AE2DAD7&ovr=6.0.1&device=Xiaomi_MI+5&net_type=1&client_id=1Yfyt44QSqu7PcVdDduBYQ%3D%3D&info_ms=fBzJ%2BCu4ZDAtl4CyHuZ%2FJQ%3D%3D&info_ma=XshbgIgi0V1HxXTqixI%2BKbgXtNtOP0%2Fn1WZtMWRWj5o%3D&mno=0&info_la=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&info_ci=9AChHTMC3uW%2BfY8%2BCFhcFw%3D%3D&mcc=0&clientversion=&bssid=VY%2BeiuZRJ%2FwaXmoLLVUrMODX1ZTf%2F2dzsWn2AOEM0I4%3D&os_level=23&os_id=dc451556fc0eeadb&resolution=1080_1920&dpi=480&client_ip=192.168.0.198&pdunid=a83d20d8',
					data: {
						hero_id: hero_id
					},
					success: (res) => {
						this.xq = res.data.info;
						console.log("---------" + this.xq);
						var textObj = JSON.stringify(this.xq);
						uni.reLaunch({
							url: "/pages/xingqin/xingqin?textObj=" + textObj
						});
					}
				});

			}
		}
	}
</script>

<style>
	page{
		/* background-color: #F8F8F8; */
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
		width: 87px;
		border-radius: 10px 10px 10px 10px;
		background-color: #FFCCCC;
	}
	.one{
		width: 98%;
		/* border: 1px solid #FFCCCC; */
		border-radius: 10px;
		margin-left: auto;
		margin-right: auto;
		margin-top: 3%;
		position: relative;
	}
	
.topimg{
	width: 100%;
	border-radius: 10px;
	
}
.one-yxzil{
	/* border: 1px solid #007AFF; */
	text-align: center;
	border-radius: 10px;
	width: 20%;
	background-color: #394554;
	/* height: 100px; */
	/* line-height: 100px; */
	position: absolute;
    bottom: 5%;
	left: 2%;
}
.pifumz{
    color: #f3c258;
	font-size: 15px;
	margin-top: 1%;
}
   .yxmz{
	color: #FFFFFF;
	font-size: 20px;
	margin-top: 1%;
	}
	.yxziliao{
		border: 1px solid #FFFFFF;
			color: #FFFFFF;
			width: 50%;
			margin-left: auto;
			margin-right: auto;
			font-size: 8px;
			margin-top: 2%;
			margin-top: 2%;
	}
	.uni-product-image {
		width: 87px;
		height: 87px;
		/* border: 1px solid rgba(255,204,204);
		border-radius: 0px 10px 0px 10px; */
		border-radius: 10px 0px 10px 0px;
	}

	.name {
		/* border: 1px solid #007AFF; */
		text-align: center;
		color: #FFFFFF;

	}

	.pifu {
		width: 100%;
		height: 95px;
		display: flex;
		justify-content: flex-start;
		/* border: 1px solid  #4CD964; */
		
		/* margin-left: auto; 
		margin-right: auto; */
		/* overflow: hidden; */
		
		/* margin-right: 0px;
	/* 	position: absolute;
		right: 0px; */
	}
 
	.pifu-view {
		/* width: 100%; */
		/* height: 70px; */
		/* border: 1px solid #007AFF; */
		margin:1%;
		/* line-height: 50px; */
		background-color: #FFCCCC;
		border-radius: 10px;
	}
.imgaview{
	width: 100%;
	height: 70px;
	border-radius: 10px;
}
.pifuimg1 {
		width: 70px;
		height: 70px;
		border-radius: 50%;
	}
	.pifuimg {
		width: 70px;
		height: 70px;
		border-radius: 10px 10px 0px 0px;
	}


	.pifu-name {
		font-size: 10px;
		text-align: center;
		/* border: 1px solid #007AFF; */
			color: #FFFFFF;
			background-color: #FFCCCC;
			/* border-radius: 0px 0px 10px 10px; */
			border-radius: 10px;
	}
	.pifudongclass{
			border: 0.5px solid #FFCCCC;
			border-radius: 10px;
			color: #9999CC;
	}

	.bian {
		border: 1px solid #007AFF;
		display: flex;
	}
	.pifuview{
		/* border: 1px solid #DD524D; */
		padding-left: 2%;
		color: #FFCCCC;
		background-color: #F8F8F8;
		border-radius: 10px 10px 0px 0px;
		font-size: 25px;
	}
	.two{
		margin-top: 3%;
		width: 95%;
		border: 1px solid #F8F8F8;
		margin-left: auto;
		margin-right: auto;
		border-radius: 10px 10px 0px 0px;
		background-color: #F8F8F8;
		box-shadow:0 1px 4px rgba(0, 0, 0, 0.3), 0 0 20px rgba(0, 0, 0, 0.1) inset;
	}
	
	.pifudongclass2{
		width: 70px;
		height: 70px;
		/* border-radius: 50%; */
		border: 2px solid #FFFFCC;
		border-radius:50%;
	}
	.there{
		/* border: 1px solid #DD524D; */
		margin-top: 3%;
		width: 95%;
		margin-left: auto;
		margin-right: auto;
		border-radius: 10px 10px 0px 0px;
		background-color: #FFCCCC;
		box-shadow:0px 15px 10px -15px #000;
		
	}
	.jinengtext{
		/* border: 1px solid #007AFF; */
		color: #FFFFFF;
		padding-left: 2%;
		font-size: 25px;
	}
	.jinenflex{
		display: flex;
		justify-content: space-around;
		margin-top: 1%;
	}
	.duixianjiqiao{
		/* border: 1px solid #3F536E; */
		margin-top: 1%;
		color: 	#F5F5F5;
	}
	.jinengname{
		/* border: 1px solid #4CD964; */
		margin-top: 1%;
		color: #FA8072;
		font-size: 20px;
		padding-left: 2%;
	}
	.shanghai{
		/* border: 1px solid #FFCCCC; */
		margin-top: 1%;
		color: #CD5C5C;
	}
	.jineng{
		/* border: 1px solid #007AFF; */
		margin-top: 1%;
		color: 	#A52A2A;
	}
/* 	.jineng-img{
		border: 1px solid #F3C258;
		margin-top: 1%;
	} */
	.si{
		margin-top: 3%;
		/* border: 1px solid #F3C258; */
		width: 95%;
		margin-left: auto;
		margin-right: auto;
		border-radius: 10px 10px 0px 0px;
		background-color: 	#FFF0F5;
			box-shadow:0px 15px 10px -15px #000;
	}
	.sifuwendapei{
		font-size: 25px;
		color: #FFCCCC;
		padding-left: 2%;
	}
	.bian1{
		
		/* border: 1px solid #F3C258; */
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
		
	}
	
	.bian-view{
		/* border: 1px solid #007AFF; */
		width: 30%;
		margin: 1%;
		text-align: center;
	}
	.fuwen-name{
		color: 	#FF0000;
	}
	.fuwen-shuxin{
		color: #9999CC;
	}
	.wu{
		margin-top: 3%;
		/* border: 1px solid #4CD964; */
		width: 95%;
		margin-left: auto;
		margin-right: auto;
		border-radius: 10px 10px 0px 0px;
		    background-color: #FFCCCC;
			box-shadow:0px 15px 10px -15px #000;
		
	}
	.chuzhuantj{
		font-size: 25px;
		padding-left: 2%;
		color: #FFFFFF;
	}
	.wuone{
		margin-top: 1%;
		display: flex;
		justify-content: space-around;		margin-top: 1%;
	}
	.wuone-item{
		border: 1px solid #FFFFCC;
		border-radius: 3px;
	}
	.pifudongclass3{
		border: 2px solid #9999CC;
		border-radius: 3px;
	}
	.witwo{
		/* border: 1px solid #DD524D; */
		margin-top: 1%;
		color: #9999CC;
		font-size: 10px;
	}
	.wu-for{
		/* border: 1px solid #007AFF; */
		display: flex;
		justify-content: space-around;
		margin-top: 1%;
	}
	.wu-for image{
		width: 40px;
		height: 40px;
		border-radius: 0px 0px 0px 0px;
	}
	.liu{
		margin-top: 3%;
		margin-bottom: 3%;
		/* border: 1px solid #4CD964; */
		width: 95%;
		margin-left: auto;
		margin-right: auto;
		border-radius: 10px 10px 0px 0px;
		background-color: #FFF0F5;
		box-shadow:0px 15px 10px -15px #000;
	}
	.yxguanxi{
	font-size: 25px;
	padding-left: 2%;
	color: #FFCCCC;
	}
	.bianliu{
		/* border: 1px solid #2C405A; */
		margin-top: 1%;
	}
	.nane-yxyx{
		font-size: 20px;
		padding-left: 2%;
		margin-top: 1%;
	}
	.liu-there{
		/* border: 1px solid #007AFF; */
		display: flex;
		justify-content: space-around;
		margin-top: 1%;
		/* background-color: ; */
		margin-top: 1%;
	}
	.liusi{
		/* border: 1px solid #007AFF; */
		text-align: center;
		background-color: #FFCCCC;
		border-radius: 10px;
		margin-top: 1%;
	}
	.liu-text{
		color: #FFFFFF;
	}
</style>
