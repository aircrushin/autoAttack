<template>
  <div id="app">
  <div class="container">
    <h1>AutoAttack</h1>
    <span>quick suggestion for your comperssor's attack and release time</span>
    <div class="workSpace">
      <span class="type"
        >Type Your BPM</span
      >
      <input
      v-model="inputBpm"
      class="input"
      size="large"
      placeholder="Please Input Your BPM"
      maxlength="3"
      width="100px"
    />
     <button class="btn" @click="GetSuggestion">Get Suggestion</button>
    </div>
    <div class="result" v-show="flag">
      <span class="re">Attack-Time:</span> {{attack}} or {{attackShort}} ms<br/>  
      <span class="re">Release-Time:</span> {{release}} or {{releaseShort}} ms<br/>  
    </div>
    <footer class="copyright">
      <span class="copy">Copyright © 2023-2024</span>&nbsp; 
      <span class="copy">AutoAttack</span>
    </footer>
  </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
const inputBpm = ref('')
var flag = ref(false)
var attack = ref(0)
var release= ref(0)
var attackShort = ref(0)
var releaseShort = ref(0)
const GetSuggestion = () => {
  var bpm : number = parseInt(inputBpm.value)
  if (isNaN(bpm)) {
    alert("Please input a valid number")
    return
  } else {
  attack.value = 60000 / (bpm * 8)
  release.value = 60000 / (bpm * 2)
  attackShort.value = 30000 / (bpm * 8)
  releaseShort.value = 30000 / (bpm * 2)
  if (bpm === 0){
    flag.value = false
  }
  flag.value = true
}
}
</script>

<style scoped>
#app{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #fff;
  height: 80vh;
}
.container{
  text-align: center;
}
h1{
  padding-top: 60px;
  font-size: 60px;
  color:#ced4da;
}
span{
  font-size: 20px;
  color:#868e96;
}
.workSpace {
  margin: 60px auto;
  width: 500px;
  height: 200px;
  border: 1px solid #ced4da;
  border-radius: 8px; /* 增加圆角 */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* 添加阴影 */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input {
  width: 60%; /* 调整输入框宽度 */
  padding: 10px 15px; /* 增加内边距 */
  margin-bottom: 15px; /* 增加底部外边距 */
  border: 1px solid #ced4da; /* 统一边框样式 */
  border-radius: 4px; /* 增加圆角 */
  box-sizing: border-box; /* 确保宽度包含padding和border */
}

.type {
  margin-bottom: 20px;
  font-weight: bold; /* 增加字体权重 */
  color: #333; /* 根据背景颜色调整文字颜色 */
}

.btn {
  padding: 10px 20px; /* 增加内边距 */
  margin: 0; /* 移除外边距 */
  border: none; /* 移除边框 */
  border-radius: 4px; /* 增加圆角 */
  background-image: linear-gradient(to right, #6dd5ed, #2193b0); /* 添加背景渐变 */
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2); /* 增加阴影 */
  color: #fff; /* 设置文字颜色 */
  font-size: 16px; /* 调整字体大小 */
  cursor: pointer; /* 改变鼠标指针样式 */
  transition: all 0.3s; /* 添加过渡效果 */
}

.btn:hover {
  background-image: linear-gradient(to right, #2193b0, #6dd5ed); /* 改变悬停时的背景渐变方向 */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3); /* 增加悬停时的阴影 */
}
.result{
  justify-content: left;
  margin-bottom: 50px;
}
.copy{
  font-size: 12px;
  color:#868e96;
}
/* 放在页面正中下端 */
.copyright{
  position: fixed;
  bottom: 20px;
  left: 0;
  width: 100%;
  text-align: center;
}
.re{
  margin-left: 20px;
  color:#333;
}
</style>