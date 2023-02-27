<template>
	<view>
		<navigationBar title="登录" navBgColor="#b895b7"></navigationBar>
		<view class="login-home padding">
			<view class="avatar">
				<image  src="../../static/img/y.jpg" mode="aspectFill"></image>
			</view>
			<form @reset="reset" @submit="submit">
				<view class="cu-form-group margin-tb login-border padding">
					<view class="title">
						<text class="cuIcon-peoplefill"></text>
					</view>

					<input class="fs-32" placeholder="账号" v-model="loginObj.account" type="nickname"
						name="account"></input>
				</view>
				<view class="cu-form-group login-border padding">
					<view class="title">
						<text class="cuIcon-mobilefill"></text>
					</view>
					<input class="fs-32" placeholder="密码" v-model="loginObj.password" type="number"
						name="password"></input>
				</view>
				<view class="flex justify-around padding-tb-lg margin-tb-lg">
					<button form-type="reset" class="btn1 cu-btn bg-pink lg" type="default">重置</button>
					<button form-type='submit' class="btn2 cu-btn bg-lvse  lg" type="default">登录</button>
				</view>
			</form>
		</view>
		
		<!-- 登陆成功消息提示 -->
		<u-toast ref="uToast"></u-toast>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				loginObj: {
					account: 'xiaotuxian001',
					password: '123456'
				}

			};
		},
		methods: {
			async submit() {
				await this.$store.dispatch('user/login', this.loginObj)
				this.$refs.uToast.show({
					type:'success',
					message:'登陆成功,正在跳转',
					complete:() => {
						uni.switchTab({
							url:'/pages/user/my'
						})
					}
				})
			},
			// 重置表单
			reset() {
				// 重置只能重置表单样式 手动清除对象里的数据
				this.loginObj.account = ''
				this.loginObj.password = ''
			},
		}
	}
</script>

<style lang="scss">
	page {
		background-color: #b895b7;
		margin-top: 100rpx;
	}

	.login-border {
		border-radius: 50rpx;
	}

.avatar{
	display: flex;
	margin-bottom: 50rpx;
	image{
		width: 250rpx;
		height: 250rpx;
		margin: auto;
		border-radius: 50%;
	}
}
</style>
