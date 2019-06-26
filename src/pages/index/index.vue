<template>
  <div @click="clickHandle">

    <swiper 
    :indicator-dots="indicatorDots"
    :autoplay="autoplay" 
    :interval="interval"
    :duration="duration"
    >
  <block v-for="img in imgUrls" :key="img">
    <swiper-item>
      <image :src="img" style="width:100%"/>
    </swiper-item>
  </block>
</swiper>

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
    <view>
      <i-card i-class="split" v-for="item in top" :key="item" :extra="item.name" :thumb="item.img">
          <view slot="content">推荐理由：{{item.remark}}</view>
          <view slot="footer">地址：{{item.address}}</view>
      </i-card>
    </view>
  </i-panel>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000,
      grids: [
        {type:'生鲜',img:'/static/images/1.png',"url":'../list/main?type=1'},
        {type:'水果',img:'/static/images/2.png',"url":'../list/main?type=2'},
        {type:'时令蔬菜',img:'/static/images/3.png',"url":'../list/main?type=3'}
      ],
      top :[
        
      ],
      imgUrls: [
      'https://images.unsplash.com/photo-1551334787-21e6bd3ab135?w=640',
      'https://images.unsplash.com/photo-1551214012-84f95e060dee?w=640',
      'https://images.unsplash.com/photo-1551446591-142875a901a1?w=640'
    ],
    indicatorDots: false,
    autoplay: false,
    interval: 5000,
    duration: 1000
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
    db.collection('top').get().then(
      res => {
        console.log(res.data)
        this.top = res.data
      }
    )
    // cloud functions
    // wx.cloud.callFunction({ name: 'me' }).then(
    //   res => { console.log(res) }
    // )

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
