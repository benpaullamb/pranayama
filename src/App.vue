<template>
  <div class="container">
    <div class="text">
      <h1 class="label">{{ labels[stateIndex] }}</h1>
      <span class="time">{{ time + 1 }}</span>
    </div>

    <div class="outerCircle">
      <div
        class="innerCircle"
        :style="{
          width: `${widths[stateIndex]}%`,
          transition: `width ${durations[stateIndex]}s linear`,
        }"
      ></div>
    </div>

    <footer class="footer">
      <span class="title">Pranayama (4/7/8 breathing)</span>
      <span class="version">For Abbie Smith &middot; v1.1.0</span>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const labels = ["Inhale", "Hold", "Exhale"];
const durations = [4, 7, 8];
const widths = [100, 100, 0];

const stateIndex = ref(0);
const time = ref(0);

onMounted(() => {
  setInterval(() => {
    time.value += 1;

    if (stateIndex.value === 0 && time.value >= durations[0]) {
      stateIndex.value = 1;
      time.value = 0;
    }

    if (stateIndex.value === 1 && time.value >= durations[1]) {
      stateIndex.value = 2;
      time.value = 0;
    }

    if (stateIndex.value === 2 && time.value >= durations[2]) {
      stateIndex.value = 0;
      time.value = 0;
    }
  }, 1000);
});
</script>

<style scoped>
.container {
  height: 100dvh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to right, #3674b5, #a1e3f9);
}

.text {
  z-index: 2;
  color: rgba(0, 0, 0, 0.8);
}

.label {
  font-weight: normal;
}

.time {
  display: block;
  text-align: center;
  font-size: 12px;
}

.outerCircle {
  width: 90%;
  aspect-ratio: 1;
  border-radius: 50%;
  background: #a1e3f9;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.innerCircle {
  aspect-ratio: 1;
  border-radius: 50%;
  background: #d1f8ef;
}

.footer {
  padding: 8px;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: rgba(0, 0, 0, 0.5);
}

.title {
  font-size: 12px;
}

.version {
  font-size: 10px;
}
</style>
