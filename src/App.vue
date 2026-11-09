<template>
  <h1>Create your own samehead</h1>

  <div class="image-container">
    <img
      v-for="(boy, i) in boys"
      :key="boy.name"
      :src="`/${boy.name}_liggur_cropped.png`"
      :style="`opacity: ${(Number(boy.opacity) * 0.1 * (10 - i * 1.5)).toFixed(3)}`"
    />
  </div>

  <div class="input-container">
    <template v-for="boy in boys">
      <label :for="boy.name + '_input'"
        >{{ boy.name }} - {{ boy.opacity }}</label
      >
      <input
        type="range"
        max="1"
        min="0"
        step="0.01"
        v-model="boy.opacity"
        :id="boy.name + '_input'"
      />
    </template>
  </div>

  <button @click="random">Random</button>

  <!--CanvasSelector :boys="boys"/-->
</template>

<script setup lang="ts">
import { ref, watch } from "vue";
import CanvasSelector from "./components/CanvasSelector.vue";

const boys = ref([
  { name: "baldur", opacity: 0.2 },
  { name: "dagur", opacity: 0.2 },
  { name: "oliver", opacity: 0.2 },
  { name: "tomas", opacity: 0.2 },
  { name: "tumi", opacity: 0.2 },
]);

const random = () => {
  boys.value.forEach((boy) => (boy.opacity = Number(Math.random().toFixed(3))));
};

let counter = 0;
const animate = () => {
  const deg = counter * (Math.PI / 180);
  const sin = Math.sin(deg);
  console.log(sin);
  boys.value.forEach((boy, i) => {
    boy.opacity = Math.abs(Math.sin(deg));
  });
  counter += 1;
  setTimeout(() => requestAnimationFrame(animate), 100);
};

animate();
</script>

<style scoped>
h1 {
  text-align: center;
  margin-bottom: 2rem;
  font-size: 2rem;
  max-width: 90vw;
}

.image-container {
  max-width: 90vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  position: relative;
  width: 32rem;
  aspect-ratio: 1;
  margin: 0 auto;

  & img {
    z-index: 50;
    inset: 0;
    width: 100%;
    max-width: 100%;
    height: 100%;
    object-fit: cover;
    position: absolute;
    opacity: 0.5;
    background-blend-mode: multiply;
  }
}

.input-container {
  display: flex;
  flex-direction: column;
}
</style>
