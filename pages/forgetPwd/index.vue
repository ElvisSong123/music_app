<template>
	<view class="reg-wrapper">
		<view class="title">
			<view>忘记密码</view>
			<view class="policy">请输入您的手机号</view>
		</view>
		<view class="reg-info">
			<view class="phone">
				<image v-if="!isPhoneEnter" src="../../static/img/reg-phone.png"></image>
				<image v-else src="../../static/img/phone-enter.png"></image>
				<input v-model="phoneValue" @input="phoneInput" type="number" placeholder="手机号">
			</view>
			<view class="validate">
				<view>
					<image v-if="!isCodeEnter" src="../../static/img/reg-validate.png"></image>
					<image v-else src="../../static/img/code-enter.png"></image>
					<input v-model="codeValue" @input="codeInput" type="number" placeholder="验证码">
				</view>
				<text v-if="!isCount" @click="getVerificationCode">获取验证码</text>
				<text v-else>重新发送({{count}})</text>
			</view>
		</view>
		<button :class="['button',{'is-not':isNotClick}]" type="primary" @click="nextStep">下一步</button>
		<view class="background">	
			<image src="../../static/img/background.png"></image>
		</view>
	</view>
</template>

<script>
	import service from '../../service.js';
	import mInput from '../../components/m-input.vue';

	export default {
		components: {
			mInput
		},
		data() {
			return {
				account: '',
				password: '',
				email: '',
				phoneValue:'',
				codeValue:'',
				isCount:false,
				count:60,
				timer:null,
				isNotClick:true,
				isPhoneEnter:false,
				isCodeEnter:false,
			}
		},
		methods: {
			nextStep(){
				if(this.phoneValue && this.codeValue){
					uni.navigateTo({
						url:"../resetPwd/index"
					})
				}
			},
			phoneInput(){
				if(this.phoneValue){
					this.isPhoneEnter = true;
				}else{
					this.isPhoneEnter = false;
				}
				if(this.phoneValue && this.codeValue){
					this.isNotClick = false;
				}else{
					this.isNotClick = true;
				}
			},
			codeInput(){
				if(this.codeValue){
					this.isCodeEnter = true;
				}else{
					this.isCodeEnter = false;
				}
				if(this.phoneValue && this.codeValue){
					this.isNotClick = false;
				}else{
					this.isNotClick = true;
				}
			},
			getVerificationCode(){
				if(!this.phoneValue) return;
				this.requestCode();
				this.countDown();
			},
			requestCode(){},
			countDown(){
				this.isCount = true;
				this.timer = setInterval(()=>{
					this.count--;
					if(this.count == 0){
						clearInterval(this.timer);
						this.isCount = false;
						this.count = 60
					}
				},1000)
			},
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
	.reg-wrapper{
		width:750rpx;
		padding:0 60rpx;
		box-sizing: border-box;
		.title{
			width:100%;
			margin-top:68rpx; 
			font-size: 48rpx;
			color:#333333;
			font-weight:bold;
			font-family:PingFang-SC-Bold;
			.policy{
				font-size:24rpx;
				margin-top:24rpx;
				color:#565656;
				font-weight: 500;
				font-family:PingFang-SC-Medium;
				text{
					color:#108EE9
				}
			}
		}
		.reg-info{
			.phone,.validate{
				display: flex;
				border-bottom:1rpx solid #EEEEEE; 
				height:80rpx;
				align-items: center;
				font-size: 34rpx;
				font-family:PingFang-SC-Medium;
				font-weight:500;
				image{
					width:32rpx;
					height:40rpx;
					margin-right:20rpx;
				}
			}
			.phone{
				margin-top:148rpx;
				margin-bottom: 58rpx;
			}
			.validate{
				view{
					display: flex;
				}
				justify-content: space-between;
				text{
					font-size:28rpx;
					font-family:PingFang-SC-Medium;
					font-weight:500;
				}
			}
			
		}
		.button{
			margin-top:100rpx;	
			background:rgba(78,170,237,1);
			border-radius:24px;
		}
		.button.is-not{
			background:#CCCCCC;
		}
		.background{
			width:100%;
			height:290rpx;
			position: absolute;
			bottom:40rpx;
			left:0;
			image{
				width:100%;
				height:100%;
			}
		}
	}
</style>
