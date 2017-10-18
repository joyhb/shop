<template>
  <div id="app">
    <top></top>
    <router-view></router-view>
    <bottom></bottom>
  </div>
</template>

<script>
import top from '@/components/header'
import bottom from '@/components/footer'
export default {
  name: 'app',
  components: {
    top,
    bottom
  }
}
</script>

<style>
body{
  background: #f6f6f6;
}
#app {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
