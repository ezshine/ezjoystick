<template>
	<view>
		<view style="width: 100%;text-align: center;padding:10px;">写实摇杆</view>
		<view style="width: 100%;height: 75px;border-bottom: 1px solid #ccc;">
			<image src="../../static/beetle.png" :style="{left:beetleLeft+'px',top:beetleTop+'px',transform:'rotate('+beetleRotate+'deg)'}" style="pointer-events: none;position: absolute;z-index: 999;width: 70px;height: 50px;"></image>
			<ezjoystick style="margin-top: 75px;margin-left: 50%;"
				:touchRadius="100"
				:ballMoveRadius="50"
				:transition="true"
				@onJoyStickUpdate="onBeetleJoystickUpdate"
				>
				<view slot="ball" style="width: 50px;height: 50px;">
					<image src="../../static/Ball.png" style="width: 100%;height: 100%;"></image>
				</view>
				<view slot="stick" style="width: 20px;height: 100%;">
					<image src="../../static/Stick.png" style="width: 100%;height: 100%;display: block;"></image>
				</view>
				<view slot="bottom" style="width: 130px;height: 130px;">
					<image src="../../static/Dock.png" style="width: 100%;height: 100%;"></image>
				</view>
			</ezjoystick>
		</view>
		<view style="width: 100%;text-align: center;padding:10px;">十字键</view>
		<view style="width: 100%;height: 75px;">
			<ezjoystick style="margin-top: 75px;margin-left: 50%;"
				:touchRadius="100"
				:ballMoveRadius="80"
				:transition="false"
				@onJoyStickUpdate="onCrossJoyStickUpdate"
				@onJoyStickCancel="onCrossJoyStickCancel"
				>
			</ezjoystick>
			<view style="position: relative;margin-top: 75px;margin-left: 50%;">
				<view style="position: absolute;width:130px;height: 130px;transform: translate(-50%,-50%);">
					<image class='corssup' src="../../static/corss_up.png" :style="{opacity:crossupPressed?.6:1}" style="width: 100%;height: 100%;position: absolute;"></image>
					<image class='corssright' src="../../static/corss_right.png" :style="{opacity:crossrightPressed?.6:1}" style="width: 100%;height: 100%;position: absolute;"></image>
					<image class='corssdown' src="../../static/corss_down.png" :style="{opacity:crossdownPressed?.6:1}" style="width: 100%;height: 100%;position: absolute;"></image>
					<image class='corssleft' src="../../static/corss_left.png" :style="{opacity:crossleftPressed?.6:1}" style="width: 100%;height: 100%;position: absolute;"></image>
					<image src="../../static/corss_bottom.png" style="width: 100%;height: 100%;position: absolute;"></image>
				</view>
			</view>
		</view>
		<view style="width: 100%;text-align: center;padding:10px;margin-top: 20px;"></view>
		<view style="width: 100%;height: 90px;">
			<ezjoystick style="margin-top: 90px;margin-left: 50%;"
				:touchRadius="110"
				:ballMoveRadius="78"
				:transition="false"
				@onJoyStickUpdate='onWZJoystickUpdate'
				>
				<view slot="ball" style="width: 50px;height: 50px;">
					<image src="../../static/wangzhe_ball.png" style="width: 100%;height: 100%;"></image>
				</view>
				<view slot="bottom" style="width: 207px;height: 207px;">
					<image src="../../static/wangzhe_bottom.png" style="width: 100%;height: 100%;"></image>
				</view>
			</ezjoystick>
			<view style="width: 250px;height: 250px;position: absolute;z-index: 99;transform: translate(25%,-50%);pointer-events: none;">
				<image src="../../static/wangzhe_arrow.png" :style="{transform:'rotate('+wangzheRotate+'deg)'}" style="width: 250px;height: 250px;"></image>
			</view>
		</view>
	</view>
</template>

<script>
	import ezjoystick from "../../components/ezjoystick.vue"
	export default {
		components:{
			ezjoystick
		},
		data() {
			return {
				crossupPressed:false,
				crossrightPressed:false,
				crossdownPressed:false,
				crossleftPressed:false,
				beetleLeft:0,
				beetleTop:0,
				beetleRotate:0,
				wangzheRotate:0
			}
		},
		onLoad() {
			
		},
		methods: {
			onWZJoystickUpdate(obj){
				this.wangzheRotate=obj.angle/(3.14159/180)+90;
			},
			onBeetleJoystickUpdate(obj){
				this.beetleLeft+=Math.cos(obj.angle)*(obj.power*10);
				this.beetleTop+=Math.sin(obj.angle)*(obj.power*10);
				this.beetleRotate=obj.angle/(3.14159/180);
			},
			onCrossJoyStickUpdate(obj){
				this.crossupPressed=false;
				this.crossrightPressed=false;
				this.crossdownPressed=false;
				this.crossleftPressed=false;
				if(obj.angle>-2.35&&obj.angle<-0.75){
					this.crossupPressed=true;
				}else if(obj.angle>-0.75&&obj.angle<0.75){
					this.crossrightPressed=true;
				}else if(obj.angle>0.75&&obj.angle<2.35){
					this.crossdownPressed=true;
				}else{
					this.crossleftPressed=true;
				}
			},
			onCrossJoyStickCancel(){
				this.crossupPressed=false;
				this.crossrightPressed=false;
				this.crossdownPressed=false;
				this.crossleftPressed=false;
			}
		}
	}
</script>

<style>
	
	page{
		width: 100%;
		height: 100%;
		overflow: hidden;
	}
	view
	{
		box-sizing: border-box;
	}
</style>
