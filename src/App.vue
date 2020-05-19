<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <move-func><button class="move-button">导航</button> </move-func>
  </div>
</template>

<script>

// movePositon="moveX"  移动方向可选,默认不限制 moveX,moveY
// styleString ="bottom: 8rem; right: 1rem;" 组件样式 (可以给定初始位置)
// 请最好给solt中的元素固定宽高 不然可能会出bug
// import HelloWorld from './components/HelloWorld.vue'
import moveFunc from './myPlugin/moveFunc/move-func'; // 引入
export default {
  name: 'App',
  components: {
    moveFunc
  },
  data() {
    return {
      styleString:""
      
    };
  }
 
}
</script>

<style scoped>
.move-button {
  position: relative;
  z-index: 1;
  width: 3rem;
  height: 3rem;
  line-height: 3rem;
  text-align: center;
  font-weight: bold;
  border-radius: 50%;
  border: none;
  color: #ffffff;
  font-size: 0.9rem;
  box-shadow: 0px 4px 8px 0px rgba(35, 65, 41, 0.42);
  background: rgba(0, 0, 0, 1);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
