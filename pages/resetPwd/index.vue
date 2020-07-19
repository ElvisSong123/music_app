<template>
	<view class="resetPwd-wrapper">
		<view class="title">
			<view>重置密码</view>
			<view class="policy">密码由8-20位数字、字母组成</text></view>
		</view>
		<view class="reg-info">
			<view class="phone">
				<image v-if="!isPasswordEnter" src="../../static/img/password.png"></image>
				<image v-else src="../../static/img/password-enter.png"></image>
				<input v-model="password" @input="phoneInput" type="text" password placeholder="密码">
			</view>
			<view class="validate">
				<view>
					<image v-if="!isPasswordAgainEnter" src="../../static/img/password.png"></image>
					<image v-else src="../../static/img/password-enter.png"></image>
					<input v-model="passwordConfirm" @input="codeInput" type="text" password placeholder="请再次输入密码">
				</view>
			</view>
		</view>
		<button :class="['button',{'is-not':isNotClick}]" type="primary" @click="nextStep">下一步</button>
		<view class="background">
			<image src="../../static/img/background.png"></image>
		</view>
		<uni-popup ref="popup" type="dialog">
			<uni-popup-dialog :type="diaType" :title="diaTitle" message="成功消息" :duration="2000" :before-close="true" @close="diaClose" @confirm="diaConfirm"></uni-popup-dialog>
		</uni-popup>
	</view>
</template>

<script>
	import service from '../../service.js';
	import mInput from '../../components/m-input.vue';
	import uniPopup from '@/components/uni-popup/uni-popup.vue';
	import uniPopupMessage from '@/components/uni-popup/uni-popup-message.vue';
	import uniPopupDialog from '@/components/uni-popup/uni-popup-dialog.vue';
	export default {
		components: {
			mInput,
			uniPopup,
			uniPopupMessage,
			uniPopupDialog
		},
		data() {
			return {
				account: '',
				password: '',
				passwordConfirm: '',
				email: '',
				timer: null,
				isNotClick: true,
				isPasswordEnter: false,
				isPasswordAgainEnter: false,
				diaType:'',
				diaTitle:'',
				pwdChangeSuccess:false,

			}
		},
		methods: {
			diaClose(done){
				done();
			},
			diaConfirm(done){
				done();
				if(this.pwdChangeSuccess){
					uni.navigateTo({
						url:"../login/login"
					})
				}
			},
			nextStep() {
				if (this.password != this.passwordConfirm) {
					this.diaType = 'warn',
					this.diaTitle = '密码输入不一致，请重新输入';
					this.pwdChangeSuccess = false;
					this.$refs.popup.open()
				}else{
					this.diaType = 'success',
					this.diaTitle = '密码修改成功,请重新登录';
					this.$refs.popup.open();
					this.pwdChangeSuccess = true;
				}
			},
			phoneInput() {
				if (this.password) {
					this.isPasswordEnter = true;
				} else {
					this.isPasswordEnter = false;
				}
				if (this.password && this.passwordConfirm) {
					this.isNotClick = false;
				} else {
					this.isNotClick = true;
				}
			},
			codeInput() {
				if (this.passwordConfirm) {
					this.isPasswordAgainEnter = true;
				} else {
					this.isPasswordAgainEnter = false;
				}
				if (this.password && this.passwordConfirm) {
					this.isNotClick = false;
				} else {
					this.isNotClick = true;
				}
			},
			requestCode() {},
			register() {
				/**
				 * 客户端对账号信息进行一些必要的校验。
				 * 实际开发中，根据业务需要进行处理，这里仅做示例。
				 */
				if (this.account.length < 5) {
					uni.showToast({
						icon: 'none',
						title: '账号最短为 5 个字符'
					});
					return;
				}
				if (this.password.length < 6) {
					uni.showToast({
						icon: 'none',
						title: '密码最短为 6 个字符'
					});
					return;
				}
				if (this.email.length < 3 || !~this.email.indexOf('@')) {
					uni.showToast({
						icon: 'none',
						title: '邮箱地址不合法'
					});
					return;
				}

				const data = {
					account: this.account,
					password: this.password,
					email: this.email
				}
				service.addUser(data);
				uni.showToast({
					title: '注册成功'
				});
				uni.navigateBack({
					delta: 1
				});
			}
		}
	}
</script>

<style lang="less">
	.resetPwd-wrapper {
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
				view {
					display: flex;
				}

				justify-content: space-between;

				text {
					font-size: 28rpx;
					font-family: PingFang-SC-Medium;
					font-weight: 500;
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
