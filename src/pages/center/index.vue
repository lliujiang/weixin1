<template>
  <div >
      <i-panel title="水果">
    <i-radio-group current="current" @change="handleFruitChange">
        <i-radio v:for="fruit" position="position" v:key="item.id" value="item.name">
        </i-radio>
    </i-radio-group>
</i-panel>

<i-button @click="handleClick" type="ghost">切换单选框位置</i-button>

<i-panel title="radio-动物">
    <i-radio :value="animal" :key="disabled" :checked="checked" @change="handleAnimalChange">
    </i-radio>
</i-panel>

<i-button @click="handleDisabled" type="ghost">切换disabled状态</i-button>
  </div>
</template>

<script>

export default {
  data () {
      return {
          fruit: [{
            id: 1,
            name: '香蕉',
        }, {
            id: 2,
            name: '苹果'
        }, {
            id: 3,
            name: '西瓜'
        }, {
            id: 4,
            name: '葡萄',
        }],
        current: '苹果',
        position: 'left',
        animal: '熊猫',
        checked: false,
        disabled: false,
      }
  },
      

  components: {
  },

  methods: {   
      handleClick() {
        this.setData({
            position: this.data.position.indexOf('left') !== -1 ? 'right' : 'left',
        });
    },
    handleDisabled() {
        this.setData({
            disabled: !this.data.disabled
        });
    },
    handleAnimalChange({ detail = {} }) {
        this.setData({
            checked: detail.current
        });
    }
  },

  created () {
  }
}
</script>

<style>
</style>