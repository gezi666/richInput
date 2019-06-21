<template>
  <div id="app">
    <h1 class="title">
      <span>手动搭建简易富文本编辑器</span>
    </h1>
    <richInput />
  </div>
</template>

<script>
import richInput from './components/richInput.vue'

export default {
  name: 'app',
  components: {
    richInput
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
}
.title{
  text-align: center
}
.title span{
  display: inline-block;
  background-image: radial-gradient(circle, #e68d8d 10%, #ffcb00 20%, #ecc815 40%, #c0d243 60%,#64e1d5 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
