<template>
	<view>
		<view>
			<view v-for="(itemzong,index) in textObj">
				<view>
					<image :src="xiandapifu"></image>
					<view>
						<view>
							{{xianmz}}
						</view>
						<view>{{itemzong.name}}</view>
						<view @click="yxzl">英雄资料</view>
						<view v-if="yxzlbool">
							<view @click="guan">X</view>
							<view>{{itemzong.background_story}}</view>
						</view>

					</view>

					<view class="pifu">
						<view>皮肤</view>
						<view v-for="(pifu,indexpifu) in pifus" class="pifu-view" @click="pifuitem(indexpifu)">
							<view>
								<image :src="pifu.big_img" class="pifuimg"></image>
							</view>
							<view class="pifu-name">{{pifu.skin_name}}</view>
						</view>
					</view>

					<view>
						<view>技能介绍</view>
						<!-- <view> -->
						<view v-for="(jinengs,indexjineng) in jineng" @click="jinengclick(indexjineng)">
							<view>
								<image :src="jinengs.icon" class="pifuimg"></image>
							</view>
						</view>
						<view>
							对线技巧:{{skill_tips}}
						</view>

						<view>
							{{jineng[jinengone].name}}
						</view>

						<view v-for="(attrsts,indexattrs) in jineng[jinengone].attrs">
							<view>{{attrsts}}</view>
						</view>

						<view>
							{{jineng[jinengone].description}}
						</view>
						<!-- </view> -->
					</view>



					<view>
						<view>
							符文搭配建议
						</view>
						<view>
							<view v-for="(rec_inscriptionst,indexrec_inscriptions) in rec_inscriptions">

								<view class="bian">
									<view v-for="(fuwen,fuwenindex) in rec_inscriptionst.list">
										<view>{{fuwen.name}}</view>
										<view>{{fuwen.attrs}}</view>
										<view>
											<image :src="fuwen.icon" class="pifuimg"></image>
										</view>
									</view>
								</view>
							</view>
						</view>
					</view>


					<view>
						<view>
							出装推荐
						</view>
						<view>
							<view v-for="(equip_choicest,indexequip_choice) in equip_choice">
								<view @click="chuzhuanclick(indexequip_choice)">{{equip_choicest.title}}</view>


							</view>
							<view class="bian">
								<view>{{description}}</view>
								<view v-for="(chuzhuan,indexchuzuan) in equip_choice[chuzhuanindex].list">
									<view>
										<image :src="chuzhuan.icon" class="pifuimg"></image>
									</view>
								</view>
							</view>
						</view>
					</view>


					<view>
						<view>英雄关系</view>
						<view class="bian">
							<view>最佳搭档</view>
							<view v-for="(partner_herost,indexpartner_hero) in partner_hero">
								<view>{{partner_herost.name}}</view>
								<view>
									<image :src="partner_herost.icon" class="pifuimg" @click="zuijia(partner_herost.hero_id)"></image>
								</view>
							</view>
						</view>

						<view class="bian">
							<view>压制英雄</view>
							<view v-for="(restrained_herost,indexrestrained_hero) in restrained_hero">
								<view>{{restrained_herost.name}}</view>
								<view>
									<image :src="restrained_herost.icon" class="pifuimg" @click="yazhi(restrained_herost.hero_id)"></image>
								</view>
							</view>
						</view>

						<view class="bian">
							<view>被压制英雄</view>
							<view v-for="(be_restrained_herost,indexbe_restrained_hero) in be_restrained_hero">
								<view>{{be_restrained_herost.name}}</view>
								<view>
									<image :src="be_restrained_herost.icon" class="pifuimg" @click="beiyazhi(be_restrained_herost.hero_id)"></image>
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
				this.yxzlbool = !this.yxzlbool;
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
		display: flex;
		justify-content: center;
	}

	.pifu-view {
		width: 70px;
		height: 70px;
		border: 1px solid #007AFF;
	}

	.pifuimg {
		width: 50px;
		height: 50px;
	}

	.pifu-name {
		font-size: 10px;
	}

	.bian {
		border: 1px solid #007AFF;
		display: flex;
	}
</style>
