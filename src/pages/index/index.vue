<template>
  <div @click="clickHandle">
    <i-notice-bar icon="systemprompt" loop>
    鲜果园特价啦！！！
    </i-notice-bar>
    <i-grid i-class="no-border">
      <i-grid-item @click="goList(item.url)" i-class="no-border" v-for="item in grids" :key="item">
          <i-grid-icon>
              <image :src="item.img" />
          </i-grid-icon>
          <i-grid-label>{{item.type}}</i-grid-label>
      </i-grid-item>
  </i-grid>
  <i-panel title="水果推荐">
      <view class="top-padding">
      <i-card title="橘子" extra="orange" thumb="/static/images/6.png">
        <view slot="content">多食易上火</view>
        <view slot="footer">鲜果园</view>
      </i-card>
      <view class="top-padding"></view>
      <i-card title="火龙果" i-class="top-padding" extra="dragon fruit" thumb="/static/images/7.png">
        <view slot="content">抗衰老,美白皮肤</view>
        <view slot="footer">鲜果园</view>
      </i-card>
      <view class="top-padding"></view>
      <i-card title="木瓜" i-class="top-padding" extra="pawpaw" thumb="/static/images/8.png">
        <view slot="content">健胃消食，抗痉挛</view>
        <view slot="footer">鲜果园</view>
      </i-card>
      <view class="top-padding"></view>
      <i-card title="桃子" i-class="top-padding" extra="peach" thumb="/static/images/9.png">
        <view slot="content">补益气血，养阴生津</view>
        <view slot="footer">鲜果园</view>
      </i-card>
      <view class="top-padding"></view>
      <i-card title="石榴" i-class="top-padding" extra="pomegranate" thumb="/static/images/10.png">
        <view slot="content">驱虫，止血</view>
        <view slot="footer">鲜果园</view>
      </i-card>
      <view class="top-padding"></view>
    </view>
    </i-panel>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      },
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000,
      grids: [
        {type:'生鲜',img:'/static/images/1.png',"url":'../list/main?type=1'},
        {type:'水果',img:'/static/images/2.png',"url":'../list/main?type=2'},
        {type:'时令蔬菜',img:'/static/images/3.png',"url":'../list/main?type=3'}
      ]
    }
  },

  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    },
    goList (url) {
      mpvue.navigateTo({ url })
    },
    goType (type) {
      let url = '../list/main?type=' + type
      mpvue.navigateTo({ url })
    }
  },

  created () {
    const db = wx.cloud.database({ env: 'liujiang-af8dd9' })
    db.collection('shop').get().then(
      res => {
        console.log(res.data)
        this.shops = res.data
      }
    )
    // cloud functions
    wx.cloud.callFunction({ name: 'me' }).then(
      res => { console.log(res) }
    )

    // let app = getApp()
  }
}
</script>

<style scoped>
div >>> .no-border {
  border-width: 0pt;
}
div >>> .top-padding {
  padding-top: 50rpx;
}
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}
.all{
  width:7.5rem;
  height:1rem;
  background-color:blue;
}
.all:after{
  display:block;
  content:'';
  clear:both;
}
.left{
  float:left;
  width:3rem;
  height:1rem;
  background-color:red;
}

.right{
  float:left;
  width:4.5rem;
  height:1rem;
  background-color:green;
}
</style>
