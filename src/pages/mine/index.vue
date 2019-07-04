<template>
  <div>
    <view class="userinfo">
    <view class="userinfo-avatar">
    <open-data type="userAvatarUrl"></open-data>
    </view>
    <open-data type="userNickName"></open-data>
    </view>
    <i-panel title="我要推荐">
    <i-input :value="name" @change="changeName($event)" title="游戏名称" autofocus placeholder="名称" maxlength="20"/>
    <i-input :value="remark" @change="changeRemark($event)" title="游戏介绍" placeholder="介绍" maxlength="20" />
    <i-input :value="address" @change="changeAddress($event)" title="游戏官网" placeholder="官网" maxlength="50" />
    <i-button @click="handleClick()">我要分享</i-button>
    <i-toast id="toast" />
    </i-panel>
  </div>
</template>

<script>
const { $Toast } = require('../../../static/dist/base/index');

export default {
  data () {
    return {
      name: "",
      address: "",
      remark: ""
    }
  },

  methods: {
    changeName(event) {
      console.log(event)
      this.name = event.mp.detail.detail.value
    },
    changeAddress(event) {
      console.log(event)
      this.address = event.mp.detail.detail.value
    },
    changeRemark(event) {
      console.log(event)
      this.remark = event.mp.detail.detail.value
    },
    handleClick() {
      if (this.name && this.address && this.remark) {
        let event = {
          name: this.name,
          address: this.address,
          remark: this.remark,
          image: 'cloud://study-7d4e04.7374-study-7d4e04-1258991960/4.png'
        }
        wx.cloud.callFunction({ name: 'wegame', data: event }).then(
              res => {
                console.log(res)
                }
        )
        $Toast({
            content: 'OK,谢谢你的分享！',
            type: 'success'
        });
      } else {
        $Toast({
            content: '有错误，请重试！',
            type: 'warning'
        });
      }
    }
  },

  created () {
  }
}
</script>

<style scoped>
.userinfo {
  position: relative;
  width: 750rpx;
  height: 320rpx;
  color: #666;
  display: flex;
  flex-direction: column;
  align-items: center;
}
 
.userinfo-avatar {
  overflow:hidden;
  display: block;
  width: 160rpx;
  height: 160rpx;
  margin: 20rpx;
  margin-top: 50rpx;
  border-radius: 50%;
  border: 2px solid #fff;
  box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.2);
}
</style>
