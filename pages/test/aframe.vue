<template lang="pug">
div
  a-scene(test-aframe)
    a-box.raycast(
      :position="`0 ${yPos} -3`",
      :rotation="`${xRot} ${yRot} ${zRot}`",
      :color="cubeColor",
      @click="logHello"
    )
    a-camera(
      wasd-controls-enabled="false",
      look-controls-enabled="false",
      cursor="rayOrigin: mouse",
      raycaster="objects: .raycast"
      position="0 0 0"
    )
</template>

<script setup lang="ts">
const yPos = ref(0);
const xRot = ref(0);
const yRot = ref(0);
const zRot = ref(0);

const colorIndex = ref(0)
const logHello = () => {
  colorIndex.value = (colorIndex.value + 1) % 3;
};
const colors = ["red", "lime", "blue"];
const cubeColor = computed(() => colors[colorIndex.value])
AFRAME.registerSystem("test-aframe", {
  tick: (time) => {
    const elapsed = time / 1000
    yPos.value = Math.sin(elapsed);
    xRot.value = elapsed * 30;
    yRot.value = elapsed * 53;
    zRot.value = elapsed * 73;
  }
})
</script>
