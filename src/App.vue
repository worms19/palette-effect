<template>
  <body>
    <div class="hello">
      <h1>Hello world</h1>
      <h1>xVal= {{ xVal }}</h1>
      <h1>yVal= {{ yVal }}</h1>
    </div>
    <div
      ref="target"
      class="big-element"
      :style="{
        '--x-pos': `${xVal}%`,
        '--y-pos': `${yVal}%`,
      }"
    >
      <div>
        <div class="red-box ul">A</div>
        <div class="red-box ur">B</div>
        <div class="red-box dl">C</div>
        <div class="red-box dr">D</div>
      </div>
    </div>
  </body>
</template>

<script setup>
import { useMouseInElement } from '@vueuse/core';
import { computed, ref } from 'vue';

const target = ref(null);
const { x, y } = useMouseInElement(target);
const a = window.screen.width;
const b = window.screen.height;

const xVal = computed(() =>
  isFinite(x.value / a) ? ((x.value / a) * -50).toFixed(3) : 0,
);
const yVal = computed(() =>
  isFinite(y.value / b) ? ((y.value / b) * -50).toFixed(3) : 0,
);
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
  overflow: hidden;
  height: 100%;
  width: 100%;
}

h1 {
  display: block;
}

.big-element {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 200vw;
  height: 200vh;
  transition: transform 1s linear;
  transform: translate(var(--x-pos), var(--y-pos));
}

.hello {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, 0);
}

.red-box {
  position: absolute;
  width: 1000px;
  height: 1000px;
  background-color: red;
}

.ul {
  top: 0;
  left: 0;
}
.ur {
  top: 0;
  right: 0;
}
.dl {
  bottom: 0;
  left: 0;
}
.dr {
  bottom: 0;
  right: 0;
}
</style>
