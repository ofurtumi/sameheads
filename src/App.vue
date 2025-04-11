<script setup lang="ts">
import { ref, watch } from "vue";

const boys = ref([
  { name: "baldur", opacity: 0.2 },
  { name: "dagur", opacity: 0.2 },
  { name: "oliver", opacity: 0.2 },
  { name: "tomas", opacity: 0.2 },
  { name: "tumi", opacity: 0.2 },
]);
</script>

<template>
  <div class="image-container">
    <img
      v-for="(boy, i) in boys"
      :key="boy"
      :src="`/${boy.name}_liggur_cropped.png`"
      :style="`opacity: ${(Number(boy.opacity) + (5 - i) * 0.01).toFixed(3)}`"
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
</template>

<style scoped>
.image-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  position: relative;
  width: 32rem;
  aspect-ratio: 1;

  & img {
    inset: 0;
    width: 100%;
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
