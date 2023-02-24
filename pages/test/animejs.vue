<template lang="pug">
div
  a-scene(light="defaultLightsEnabled: false")
    a-box.raycast(
      :position="`0 ${posRots.posY} -3`",
      :rotation="`${posRots.rotX} ${posRots.rotY} ${posRots.rotZ}`",
      :color="cubeColor",
      @click="changeColor"
    )
    a-entity(light="color: #AFA; intensity: 1" position="-1 0 1")
    a-entity(light="color: #AFA; intensity: 1" position="1 0 2")
    a-entity(light="type:directional; color: #AFA; intensity: 1" position="0 1 0")
    //- a-entity(light="color: #AFA; intensity: 1.5" position="1 0 0")
    a-camera(
      wasd-controls-enabled="false",
      look-controls-enabled="false",
      cursor="rayOrigin: mouse",
      raycaster="objects: .raycast"
      position="0 0 0"
    )
    a-sky(color="#00DDDD")
</template>

<script setup lang="ts">
import anime from "animejs";
const posRots = reactive({
  posY: -1,
  rotX: 0,
  rotY: 30,
  rotZ: 0
})

const colorIndex = ref(0)
const changeColor = () => {
  colorIndex.value = (colorIndex.value + 1) % 3;
};

const colors = ["red", "lime", "blue"];
const cubeColor = computed(() => colors[colorIndex.value])
anime({
  targets: posRots,
  keyframes: [
    { posY: 1, rotZ: 180, rotX: 60, rotY: 0 },
    { posY: -1, rotZ: 0, rotX: 0, rotY: 30 }
  ],
  duration: 3000,
  easing: "easeInOutElastic",
  loop: true
})

// AFRAME.registerSystem("test-animejs", {
//   tick: (time) => {
//     const elapsed = time / 1000
//     yPos.value = Math.sin(elapsed);
//     xRot.value = elapsed * 30;
//     yRot.value = elapsed * 53;
//     zRot.value = elapsed * 73;
//   }
// })
</script>
