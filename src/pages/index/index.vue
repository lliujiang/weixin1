<template>
  <div>
    <swiper
      :indicator-dots="indicatorDots"
      :autoplay="autoplay"
      :interval="interval"
      :duration="duration"
    >
      <block v-for="img in imgUrls" :key="img">
        <swiper-item>
          <image :src="img" style="width:100%" />
        </swiper-item>
      </block>
    </swiper>
    <i-grid i-class="no-border">
    <i-grid-item @click="goType(grid)" v-for="grid in grids" :key="grid" i-class="no-border">
        <i-grid-icon>
            <image :src="grid.image" />
        </i-grid-icon>
        <i-grid-label>{{grid.title}}</i-grid-label>
    </i-grid-item>
  </i-grid>
  <i-panel :title="title_name">
    <view style="padding: 15px;">
      <i-card v-for="item in some" :key="item" i-class="split" :extra="item.name" :thumb="item.image">
          <view slot="content">{{item.remark}}</view>
          <view slot="footer">{{item.address}}</view>
      </i-card>
    </view>
  </i-panel>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title_name: "热门",
      grids: [
        {title:"RPG",image:"/static/images/1.png"},
        {title:"FTG",image:"/static/images/2.png"},
        {title:"STG",image:"/static/images/3.png"},
        {title:"MOBA",image:"/static/images/4.png"}
      ],
      some: [
    {name:"英雄联盟",address:"https://lol.qq.com/",image:"https://ossweb-img.qq.com/images/lol/v3/logo.png",remark:"《英雄联盟》(简称LOL)是由美国拳头游戏(Riot Games)开发、中国大陆地区腾讯游戏代理运营的英雄对战MOBA竞技网游。游戏里拥有数百个个性英雄，并拥有排位系统、符文系统等特色养成系统。"},
    {name:"《怪物猎人：世界(Monster Hunter:World)》",address:"http://www.capcom.co.jp/monsterhunter/world/",image:"http://www.capcom.co.jp/monsterhunter/world/pc/images/logo_title.png",remark:"《怪物猎人：世界(Monster Hunter:World)》是由CAPCOM制作发行的一款动作冒险类游戏，最多支持4人联机。游戏中，玩家可以武装自己完成各项任务与各类可怕的怪物们战斗，在游戏的过程中逐步提升自己的狩猎技巧。玩家在游戏中将扮演一位猎人，需要要探索一片新发现的神秘土地，关于这片土地人们知之甚少，所以将这片大陆称为“新世界”。猎人们必须利用他们的聪明才智和个人能力才能在激烈、变化多端的战斗中存活下来，并且最终成为终极猎人"}
    ],
      imgUrls: [
        'http://img4.imgtn.bdimg.com/it/u=1164362488,3329898880&fm=26&gp=0.jpg',
        'http://www.3dmgame.com/uploads/allimg/170614/342_170614135822_1.jpg',
        'https://img.3dmgame.com/uploads/images/news/20190628/1561717013_651314.png'
      ],
      indicatorDots: false,
      autoplay: false,
      interval: 5000,
      duration: 1000
    }
  },

  methods: {
    goType(type){
      console.log(type)
      let url = '../list/main?type=' + type.title
      mpvue.navigateTo({ url })
    }
  },

  created () {
    const db = wx.cloud.database({ env: 'study-7d4e04' })
    db.collection('some').get().then(
      res => {
        console.log(res.data)
        this.top = res.data
      }
    )

  }
}
</script>

<style scoped>
div >>> .no-border {
  border-width: 0pt;
}
div >>> .split {
  margin-bottom: 10pt;
}
</style>
