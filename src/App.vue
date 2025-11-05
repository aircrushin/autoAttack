<template>
  <div id="app">
    <!-- Geometric decorative elements -->
    <div class="geometric-shapes">
      <div class="shape circle-1"></div>
      <div class="shape circle-2"></div>
      <div class="shape triangle-1"></div>
      <div class="shape triangle-2"></div>
      <div class="shape square-1"></div>
      <div class="shape square-2"></div>
      <div class="shape squiggle-1"></div>
      <div class="shape squiggle-2"></div>
    </div>

    <div class="container">
      <!-- Post-modern header with mixed typography -->
      <div class="header-section">
        <h1 class="main-title">
          <span class="title-auto">Auto</span><span class="title-attack">Attack</span>
        </h1>
        <div class="subtitle-box">
          <span class="subtitle">COMPRESSOR TIMING</span>
          <span class="subtitle-detail">ATTACK · RELEASE · PRECISION</span>
        </div>
      </div>

      <!-- Asymmetric workspace with bold styling -->
      <div class="workSpace">
        <div class="workspace-header">
          <div class="header-bar"></div>
          <span class="type">YOUR BPM</span>
          <div class="header-bar"></div>
        </div>

        <div class="input-wrapper">
          <input
            v-model="inputBpm"
            class="input"
            placeholder="120"
            maxlength="3"
          />
          <div class="input-decoration"></div>
        </div>

        <button class="btn" @click="GetSuggestion">
          <span class="btn-text">GET SUGGESTION</span>
          <div class="btn-decoration"></div>
        </button>
      </div>

      <!-- Results section with post-modern cards -->
      <div class="result" v-show="flag">
        <div class="result-grid">
          <div class="result-card attack-card">
            <div class="card-header">ATTACK</div>
            <div class="card-values">
              <span class="value-primary">{{attack}}</span>
              <span class="value-unit">MS</span>
            </div>
            <div class="card-alt">
              <span class="alt-label">ALT:</span>
              <span class="alt-value">{{attackShort}}</span>
            </div>
            <div class="card-decoration"></div>
          </div>

          <div class="result-card release-card">
            <div class="card-header">RELEASE</div>
            <div class="card-values">
              <span class="value-primary">{{release}}</span>
              <span class="value-unit">MS</span>
            </div>
            <div class="card-alt">
              <span class="alt-label">ALT:</span>
              <span class="alt-value">{{releaseShort}}</span>
            </div>
            <div class="card-decoration"></div>
          </div>
        </div>
      </div>

      <footer class="copyright">
        <div class="footer-decoration"></div>
        <span class="copy">© 2023-2024 AutoAttack</span>
        <div class="footer-decoration"></div>
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
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;500;700&family=Audiowide&family=Bebas+Neue&display=swap');

/* Post-Modern Color Palette */
:root {
  --neon-pink: #FF006E;
  --neon-cyan: #00F5FF;
  --neon-purple: #8338EC;
  --neon-yellow: #FFBE0B;
  --hot-orange: #FB5607;
  --electric-blue: #3A86FF;
  --lime-green: #06FFA5;
  --dark-bg: #1a0033;
  --light-cream: #FFF8F0;
}

#app {
  font-family: 'Space Grotesk', 'Helvetica', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: linear-gradient(135deg, #1a0033 0%, #2d0a4e 50%, #1a0033 100%);
  min-height: 100vh;
  overflow-x: hidden;
  position: relative;
}

/* Geometric Background Shapes - Memphis Design */
.geometric-shapes {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 0;
  pointer-events: none;
}

.shape {
  position: absolute;
  animation: float 8s ease-in-out infinite;
}

.circle-1 {
  width: 200px;
  height: 200px;
  border: 8px solid var(--neon-pink);
  border-radius: 50%;
  top: 10%;
  left: 5%;
  animation: float 6s ease-in-out infinite, rotate 20s linear infinite;
}

.circle-2 {
  width: 120px;
  height: 120px;
  background: radial-gradient(circle, var(--neon-cyan) 0%, transparent 70%);
  border-radius: 50%;
  bottom: 15%;
  right: 10%;
  animation: float 8s ease-in-out infinite reverse, pulse 3s ease-in-out infinite;
}

.triangle-1 {
  width: 0;
  height: 0;
  border-left: 80px solid transparent;
  border-right: 80px solid transparent;
  border-bottom: 140px solid var(--neon-yellow);
  opacity: 0.3;
  top: 40%;
  right: 8%;
  animation: float 10s ease-in-out infinite, rotate 15s linear infinite reverse;
}

.triangle-2 {
  width: 0;
  height: 0;
  border-left: 60px solid transparent;
  border-right: 60px solid transparent;
  border-bottom: 100px solid var(--electric-blue);
  opacity: 0.4;
  bottom: 30%;
  left: 10%;
  animation: float 7s ease-in-out infinite;
}

.square-1 {
  width: 100px;
  height: 100px;
  background: linear-gradient(45deg, var(--hot-orange), var(--neon-pink));
  transform: rotate(25deg);
  top: 60%;
  left: 15%;
  opacity: 0.2;
  animation: float 9s ease-in-out infinite, rotate 25s linear infinite;
}

.square-2 {
  width: 80px;
  height: 80px;
  border: 6px solid var(--lime-green);
  transform: rotate(45deg);
  top: 20%;
  right: 20%;
  animation: float 11s ease-in-out infinite reverse;
}

.squiggle-1 {
  width: 150px;
  height: 150px;
  border: 5px dashed var(--neon-cyan);
  border-radius: 50% 50% 0 50%;
  top: 15%;
  right: 35%;
  opacity: 0.4;
  animation: float 7s ease-in-out infinite, wiggle 4s ease-in-out infinite;
}

.squiggle-2 {
  width: 100px;
  height: 100px;
  border: 4px dotted var(--neon-yellow);
  border-radius: 0 50% 50% 50%;
  bottom: 25%;
  left: 30%;
  opacity: 0.3;
  animation: float 8s ease-in-out infinite reverse;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) translateX(0px); }
  50% { transform: translateY(-30px) translateX(20px); }
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% { opacity: 0.3; transform: scale(1); }
  50% { opacity: 0.6; transform: scale(1.1); }
}

@keyframes wiggle {
  0%, 100% { transform: rotate(0deg); }
  25% { transform: rotate(5deg); }
  75% { transform: rotate(-5deg); }
}

.container {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 20px;
}

/* Post-Modern Typography */
.header-section {
  padding-top: 40px;
  margin-bottom: 50px;
  transform: skewY(-1deg);
}

.main-title {
  font-family: 'Bebas Neue', 'Audiowide', sans-serif;
  font-size: 90px;
  margin: 0;
  letter-spacing: 8px;
  text-transform: uppercase;
  line-height: 0.9;
  filter: drop-shadow(0 0 20px rgba(255, 0, 110, 0.5));
}

.title-auto {
  background: linear-gradient(135deg, var(--neon-pink), var(--hot-orange));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 700;
  display: inline-block;
  transform: skewX(-5deg);
}

.title-attack {
  background: linear-gradient(135deg, var(--neon-cyan), var(--electric-blue));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 700;
  display: inline-block;
  transform: skewX(5deg);
}

.subtitle-box {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-top: 20px;
}

.subtitle {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 24px;
  font-weight: 700;
  letter-spacing: 6px;
  color: var(--neon-yellow);
  text-shadow: 0 0 10px rgba(255, 190, 11, 0.5);
}

.subtitle-detail {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 14px;
  font-weight: 300;
  letter-spacing: 3px;
  color: var(--neon-cyan);
  opacity: 0.8;
}

/* Asymmetric Workspace */
.workSpace {
  margin: 50px auto;
  width: 550px;
  padding: 50px 40px;
  background: linear-gradient(135deg, rgba(255, 0, 110, 0.1) 0%, rgba(131, 56, 236, 0.1) 100%);
  border: 5px solid var(--neon-pink);
  border-radius: 0 30px 0 30px;
  box-shadow:
    0 0 40px rgba(255, 0, 110, 0.3),
    0 20px 60px rgba(0, 0, 0, 0.5),
    inset 0 0 40px rgba(255, 255, 255, 0.05);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  transform: rotate(-1deg);
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.workSpace:hover {
  transform: rotate(0deg) translateY(-5px);
  box-shadow:
    0 0 60px rgba(255, 0, 110, 0.5),
    0 25px 70px rgba(0, 0, 0, 0.6),
    inset 0 0 40px rgba(255, 255, 255, 0.08);
}

.workspace-header {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 30px;
  width: 100%;
  justify-content: center;
}

.header-bar {
  width: 60px;
  height: 4px;
  background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
  box-shadow: 0 0 10px var(--neon-cyan);
}

.type {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 28px;
  font-weight: 700;
  letter-spacing: 4px;
  color: var(--neon-cyan);
  text-shadow: 0 0 15px rgba(0, 245, 255, 0.6);
}

.input-wrapper {
  position: relative;
  width: 100%;
  margin-bottom: 30px;
}

.input {
  width: 80%;
  padding: 20px 30px;
  font-family: 'Space Grotesk', monospace;
  font-size: 32px;
  font-weight: 700;
  text-align: center;
  background: rgba(0, 0, 0, 0.5);
  border: 4px solid var(--electric-blue);
  border-radius: 15px;
  color: var(--neon-yellow);
  box-shadow:
    0 0 20px rgba(58, 134, 255, 0.4),
    inset 0 0 20px rgba(0, 0, 0, 0.3);
  transition: all 0.3s ease;
  letter-spacing: 4px;
}

.input:focus {
  outline: none;
  border-color: var(--neon-pink);
  box-shadow:
    0 0 30px rgba(255, 0, 110, 0.6),
    inset 0 0 20px rgba(255, 0, 110, 0.1);
  transform: scale(1.02);
}

.input::placeholder {
  color: rgba(255, 190, 11, 0.4);
  font-weight: 500;
}

.input-decoration {
  position: absolute;
  bottom: -10px;
  right: 10%;
  width: 30px;
  height: 30px;
  background: var(--lime-green);
  border-radius: 50%;
  box-shadow: 0 0 20px var(--lime-green);
}

/* Post-Modern Button */
.btn {
  position: relative;
  padding: 18px 60px;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 22px;
  font-weight: 700;
  letter-spacing: 3px;
  border: none;
  border-radius: 50px 0 50px 0;
  background: linear-gradient(135deg, var(--neon-pink), var(--hot-orange), var(--neon-yellow));
  background-size: 200% 200%;
  color: #1a0033;
  cursor: pointer;
  box-shadow:
    0 8px 30px rgba(255, 0, 110, 0.4),
    0 0 40px rgba(255, 190, 11, 0.3);
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  overflow: hidden;
  transform: skewX(-5deg);
}

.btn-text {
  position: relative;
  z-index: 1;
  display: inline-block;
  transform: skewX(5deg);
}

.btn-decoration {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 0;
  height: 0;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  transition: width 0.6s, height 0.6s;
}

.btn:hover {
  background-position: 100% 0;
  transform: skewX(-5deg) scale(1.08) translateY(-3px);
  box-shadow:
    0 15px 50px rgba(255, 0, 110, 0.6),
    0 0 60px rgba(255, 190, 11, 0.5);
}

.btn:hover .btn-decoration {
  width: 400px;
  height: 400px;
}

.btn:active {
  transform: skewX(-5deg) scale(1.02) translateY(-1px);
}

/* Post-Modern Result Cards */
.result {
  margin: 60px auto 80px;
  max-width: 800px;
}

.result-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 40px;
  padding: 0 20px;
}

.result-card {
  position: relative;
  padding: 40px 30px;
  background: linear-gradient(135deg, rgba(0, 245, 255, 0.1) 0%, rgba(58, 134, 255, 0.1) 100%);
  border: 5px solid;
  border-radius: 20px 0 20px 0;
  box-shadow:
    0 10px 40px rgba(0, 0, 0, 0.4),
    inset 0 0 30px rgba(255, 255, 255, 0.05);
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  overflow: hidden;
}

.attack-card {
  border-color: var(--neon-pink);
  transform: rotate(1deg);
}

.attack-card:hover {
  transform: rotate(0deg) translateY(-10px);
  box-shadow:
    0 20px 60px rgba(255, 0, 110, 0.5),
    inset 0 0 40px rgba(255, 0, 110, 0.1);
}

.release-card {
  border-color: var(--neon-cyan);
  transform: rotate(-1deg);
}

.release-card:hover {
  transform: rotate(0deg) translateY(-10px);
  box-shadow:
    0 20px 60px rgba(0, 245, 255, 0.5),
    inset 0 0 40px rgba(0, 245, 255, 0.1);
}

.card-header {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 32px;
  font-weight: 700;
  letter-spacing: 4px;
  margin-bottom: 20px;
  text-transform: uppercase;
}

.attack-card .card-header {
  color: var(--neon-pink);
  text-shadow: 0 0 20px rgba(255, 0, 110, 0.6);
}

.release-card .card-header {
  color: var(--neon-cyan);
  text-shadow: 0 0 20px rgba(0, 245, 255, 0.6);
}

.card-values {
  display: flex;
  align-items: baseline;
  justify-content: center;
  gap: 10px;
  margin-bottom: 15px;
}

.value-primary {
  font-family: 'Space Grotesk', monospace;
  font-size: 48px;
  font-weight: 700;
  color: var(--neon-yellow);
  text-shadow: 0 0 15px rgba(255, 190, 11, 0.6);
  letter-spacing: 2px;
}

.value-unit {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 24px;
  font-weight: 500;
  color: var(--lime-green);
  opacity: 0.8;
}

.card-alt {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 10px;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 8px;
  margin-top: 15px;
}

.alt-label {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 14px;
  font-weight: 700;
  letter-spacing: 2px;
  color: var(--electric-blue);
}

.alt-value {
  font-family: 'Space Grotesk', monospace;
  font-size: 20px;
  font-weight: 700;
  color: var(--neon-yellow);
}

.card-decoration {
  position: absolute;
  bottom: 10px;
  right: 10px;
  width: 40px;
  height: 40px;
  border: 4px solid;
  border-radius: 50%;
  opacity: 0.3;
}

.attack-card .card-decoration {
  border-color: var(--neon-pink);
}

.release-card .card-decoration {
  border-color: var(--neon-cyan);
}

/* Footer */
.copyright {
  position: fixed;
  bottom: 30px;
  left: 0;
  width: 100%;
  text-align: center;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 15px;
}

.footer-decoration {
  width: 50px;
  height: 3px;
  background: linear-gradient(90deg, transparent, var(--neon-purple), transparent);
  box-shadow: 0 0 10px var(--neon-purple);
}

.copy {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 2px;
  color: var(--neon-purple);
  text-shadow: 0 0 10px rgba(131, 56, 236, 0.5);
}

/* Responsive Design */
@media (max-width: 768px) {
  .main-title {
    font-size: 60px;
  }

  .workSpace {
    width: 90%;
    padding: 40px 20px;
  }

  .result-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .geometric-shapes .shape {
    opacity: 0.3;
    transform: scale(0.7);
  }
}
</style>