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
  attack.value = 60000 / (bpm * 16)
  release.value = 60000 / (bpm * 4)
  attackShort.value = 30000 / (bpm * 16)
  releaseShort.value = 30000 / (bpm * 4)
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
  color:#444;
}
span{
  font-size: 20px;
  font-style: italic;
  color:#868e96;
}
.workSpace {
  margin: 60px auto;
  width: 500px;
  height: 200px;
  border: 1px solid #ced4da;
  border-radius: 8px; 
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); 
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.input {
  width: 60%;
  padding: 10px 15px; 
  margin-bottom: 15px; 
  border: 1px solid #ced4da; 
  border-radius: 4px; 
  box-sizing: border-box; 
}

.type {
  margin-bottom: 20px;
  font-weight: bold; 
  color: #333; 
}

.btn {
  padding: 10px 20px;
  margin: 0; 
  border: none; 
  border-radius: 4px; 
  background-image: linear-gradient(to right, #6dd5ed, #2193b0);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2); 
  color: #fff; 
  font-size: 16px; 
  cursor: pointer; 
  transition: all 0.3s; 
}

.btn:hover {
  transform: scale(1.05);
}

.result{
  justify-content: left;
  margin-bottom: 50px;
}
.copy{
  font-size: 12px;
  color:#868e96;
}

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