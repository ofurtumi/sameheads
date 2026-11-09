<template>
  <canvas width="500" height="500" ref="canvas" id="canvas"> </canvas>
</template>

<script setup lang="ts">
import { computed, useTemplateRef, watch, type PropType } from "vue";

const props = defineProps({
  boys: {
    type: Array as PropType<{ name: string; opacity: number }[]>,
    required: true,
  },
});

const canvasRef = useTemplateRef("canvas");
const ctx = computed(() => canvasRef.value?.getContext("2d"));

watch(ctx, () => {
  initCanvas()
});

const initCanvas = () => {
  const c = ctx.value!;
  c.fillStyle = "white";

  const centerX = 250; // Center of the circle
  const centerY = 250; // Center of the circle
  const radius = 200;  // Radius of the circle
  const numSides = 5;  // Number of sides for the pentagon

  for (let i = 0; i < numSides; i++) {
    const angle = (2 * Math.PI / numSides) * i; // Angle for each vertex
    const x = centerX + radius * Math.cos(angle);
    const y = centerY + radius * Math.sin(angle);

    c.beginPath();
    c.arc(x, y, 5, 0, Math.PI * 2); // Draw a small circle at each vertex
    c.fill();
  }
};
</script>

<style scoped>
#canvas {
  border: 1px solid black;
  border-radius: 50%;
}
</style>
