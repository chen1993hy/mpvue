

<template>
  <div>
    <div class="auth_btn_bg">
      <div class="auth_btn_div">
        <div class="auth_btn_title">微信授权</div>
        <div class="auth_btn_content">
          <div class="h2">为了更快的给您提供免注册服务，我们需要授权获得以下信息。</div>
          <div class="p">您微信的公开信息（昵称、头像等）</div>
        </div>
        <div class="auth_btn_btn_div">
          <div class="cancel_btn " @click="cancelClick">取消</div>
          <button open-type="getUserInfo" @getuserinfo="authGetUserInfo">获取基础信息</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  methods: {
    cancelClick () {
      console.log('login cancelClick')
      this.$emit('cancelClick')
    },
    authGetUserInfo: function (res) {
      console.log('authGetUserInfo:', res)
      if (res.target.userInfo) {
        this.$emit('successLogin')
      } else {
        console.log('wx login error !!!!')
      }
    }
  }
}
</script>

<style scoped>
/* 微信授权弹层 */
.auth_btn_bg {
  background-color: rgba(0, 0, 0, 0.4);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 2999;
}
.auth_btn_div {
  background-color: white;
  position: fixed;
  left: 5%;
  width: 90%;
  z-index: 3000;
  top: 50%;
  margin-top: -200rpx;
  border-radius: 10rpx;
}
.auth_btn_title {
  height: 100rpx;
  font-size: 16px;
  line-height: 100rpx;
  text-align: center;
  border-bottom: 1rpx solid #f1f1f1;
}
.auth_btn_content {
  padding: 40rpx 40rpx;
}
.auth_btn_content .h2 {
  border-bottom: 1rpx solid #f1f1f1;
  padding-bottom: 16rpx;
  margin-bottom: 20rpx;
  font-size: 28rpx;
}
.auth_btn_content .p {
  font-size: 24rpx;
  color: #666;
}
.auth_btn_btn_div {
  display: flex;
  flex-direction: row;
  border-top: 1rpx solid #f1f1f1;
}

.cancel_btn{
  display: flex;
	align-items: center;
	justify-content: center;
  width:50%;
  color:#ababab;
  padding:10rpx 0;
  font-size:30rpx;
  border-right:1px solid #f5f5f5;
}

.auth_btn_btn_div button {
  background: white;
  font-size: 30rpx;
  width:50%;
  color: #2f9833;
  padding: 10rpx 0;
  border: none;
}
.auth_btn_btn_div button::after{
  border: none;
}
</style>