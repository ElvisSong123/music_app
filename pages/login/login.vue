<template>
	<view class="login-wrapper">
		<view class="title">
			<view>登录</view>
		</view>
		<view class="reg-info">
			<view class="phone">
				<image v-if="!isPhoneInput" src="../../static/img/reg-phone.png"></image>
				<image v-else src="../../static/img/phone-enter.png"></image>
				<input v-model="phoneValue" @input="phoneInput" type="number" placeholder="手机号">
			</view>
			<view class="validate">
				<view>
					<image v-if="!isPasswordInput" src="../../static/img/password.png"></image>
					<image v-else src="../../static/img/password-enter.png"></image>
					<input v-model="password" @input="passwordInput" :password="!isSeePassword" type="text" placeholder="密码">
				</view>
				<text v-if="!isPasswordInput" @click="navToForgetPassword">忘记密码</text>
				<view v-else class="logo">
					<image @touchstart="seePassword" @touchend="closePassword" class="eyes" src="../../static/img/eyes.png"></image>
					<image @click="clearPassword" class="close" src="../../static/img/close.png"></image>
				</view>
			</view>
		</view>
		<button :class="['button',{'is-not':isNotClick}]" type="primary">下一步</button>
		<view class="background">
			<image src="../../static/img/background.png"></image>
		</view>
	</view>
</template>

<script>
	import service from '../../service.js';
	import {
		mapState,
		mapMutations
	} from 'vuex'
	import mInput from '../../components/m-input.vue'

	export default {
		components: {
			mInput
		},
		data() {
			return {
				phoneValue: '',
				password: '',
				isPasswordInput: false,
				isPhoneInput:false,
				isNotClick: true,
				isSeePassword:false,
			}
		},
		computed: mapState(['forcedLogin']),
		methods: {
			navToForgetPassword(){ 
				uni.navigateTo({
					url:'../forgetPwd/index'
				})
			},
			phoneInput() {
				if (this.phoneValue) {
					this.isPhoneInput = true;
				}else{
					this.isPhoneInput = false;
				}
				if (this.phoneValue && this.password) {
					this.isNotClick = false;
				} else {
					this.isNotClick = true;
				}
			},
			passwordInput() {
				if (this.password) {
					this.isPasswordInput = true;
				}else{
					this.isPasswordInput = false;
				}
				if (this.phoneValue && this.password) {
					this.isNotClick = false;
				} else {
					this.isNotClick = true;
				}
			},
			seePassword(){
				this.isSeePassword = true;
			},
			closePassword(){
				this.isSeePassword = false;
			},
			clearPassword(){
				this.password = '';
				this.isPasswordInput = false;
			},
			initPosition() {
				/**
				 * 使用 absolute 定位，并且设置 bottom 值进行定位。软键盘弹出时，底部会因为窗口变化而被顶上来。
				 * 反向使用 top 进行定位，可以避免此问题。
				 */
				this.positionTop = uni.getSystemInfoSync().windowHeight - 100;
			},

		},
		onReady() {
			this.initPosition();
			// #ifdef MP-WEIXIN
			this.isDevtools = uni.getSystemInfoSync().platform === 'devtools';
			// #endif
		}
	}
</script>

<style lang="less">
	.login-wrapper {
		width: 750rpx;
		padding: 0 60rpx;
		box-sizing: border-box;

		.title {
			width: 100%;
			margin-top: 68rpx;
			font-size: 48rpx;
			color: #333333;
			font-weight: bold;
			font-family: PingFang-SC-Bold;

			.policy {
				font-size: 24rpx;
				margin-top: 24rpx;
				color: #565656;
				font-weight: 500;
				font-family: PingFang-SC-Medium;

				text {
					color: #108EE9
				}
			}
		}

		.reg-info {

			.phone,
			.validate {
				display: flex;
				border-bottom: 1rpx solid #EEEEEE;
				height: 80rpx;
				align-items: center;
				font-size: 34rpx;
				font-family: PingFang-SC-Medium;
				font-weight: 500;

				image {
					width: 32rpx;
					height: 40rpx;
					margin-right: 20rpx;
				}
			}

			.phone {
				margin-top: 148rpx;
				margin-bottom: 58rpx;
			}

			.validate {
				display: flex;

				view {
					display: flex;
				}

				justify-content: space-between;
				align-items: center;

				text {
					font-size: 28rpx;
					font-family: PingFang-SC-Medium;
					font-weight: 500;
				}

				.logo {
					display: flex;
					align-items: flex-end;
					height:50rpx;
					.eyes {
						width: 40rpx;
						height: 30rpx;
					}

					.close {
						width: 32rpx;
						height: 32rpx;
					}


				}
			}

		}

		.button {
			margin-top: 100rpx;
			background: rgba(78, 170, 237, 1);
			border-radius: 24px;
		}

		.button.is-not {
			background: #CCCCCC;
		}

		.background {
			width: 100%;
			height: 290rpx;
			position: absolute;
			bottom: 40rpx;
			left: 0;

			image {
				width: 100%;
				height: 100%;
			}
		}
	}
</style>
