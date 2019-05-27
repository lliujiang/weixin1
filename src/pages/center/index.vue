<template>
  <div >
    <i-cell-group>
      <i-cell title="基本用法">
        <i-rate 
            @change="onChange1" 
            :value="starIndex1">
        </i-rate>
    </i-cell>
    </i-cell-group>
  </div>
</template>

<script>

export default {
  data () {
    
      return {
        starIndex1 : 0
    }
  },
      

  components: {
  },

  methods: {   
    onChange1(e){
        console.log(e)
        const index = e.mp.detail.index;
        this.starIndex1=index
    }
  },

  created () {
  }
}
</script>

<style>
</style>