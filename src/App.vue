<template id="app">
  <!-- 页面主体 -->
  <div :style="bgImg">
    <!-- 主页头部 -->
    <main-header></main-header>
    <!-- 主页待办事项 -->
    <main-to-do></main-to-do>
    <!-- 主页底部 -->
    <!-- <main-footer></main-footer> -->
  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import MainToDo from './components/MainToDo/MainToDo.vue'
import MainFooter from './components/MainFooter.vue'

export default {
  name: 'App',
  components:{
    MainHeader:MainHeader,
    MainToDo:MainToDo,
    MainFooter:MainFooter
  },
  data() {
    return {
      // 背景图片
      bgImg: {
        backgroundImage: "url(" + require("../src/assets/bg3.jpeg") + ")",
        backgroundRepeat: "no-repeat",
        height: "600px",
        width: "100%",
        backgroundSize: "cover"
        }
     }
 },
}

</script>

<style scoped>
</style>
