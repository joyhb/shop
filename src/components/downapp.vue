<template>
  <div class="downapp" v-if="ishow">
      <div class="content">
        <a class="close" href="javascript:void(0);" @click="close"><img src="../assets/images/close.png" alt=""></a>
        <router-link :to="{ name: '', params: {} }"><img src="../assets/images/app.jpg" alt=""></router-link>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      ishow: false
    }
  },
  methods: {
    openDown () {
      this.ishow = true
      return
    },
    close: function () {
      this.ishow = false
    }
  },
  created () {
    this.openDown()
  }
}
</script>

<style lang="css" scoped>
.downapp{
  position: fixed;
  z-index: 999;
  bottom: 0;
  left: 0;
  height: 100px;
  text-align: center;
  width: 100%;
  background: rgba(51,51,51,0.82);
}
.content{
  position: relative;
  zoom: 1;
  width: 960px;
  margin: 0 auto;
  padding: 8px 0 0;
}
.close{
  position: absolute;
  right: 0px;
  top: 5px;
}
</style>
