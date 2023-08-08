<template>
  <section class="rain">
    <div
      class="rain__item"
      :style="`left:${icon.left};top:${icon.top}px;`"
      v-for="icon in arr"
      :key="icon"
    >
      <img :src="icon.img" alt="" />
    </div>
  </section>
</template>

<script setup>
import rainIcon from "./assets/img/droplet-solid.svg";
import { ref } from "vue";

let arr = ref([]);

function rainCap() {
  arr.value.push({
    img: rainIcon,
    left: `${Math.floor(Math.random() * window.innerWidth)}px`,
    top: 0,
  });
  arr.value.forEach((el) => {
    if (el.top >= window.innerHeight) {
      arr.value.splice(el, 1);
    }
  });

  setTimeout(() => {
    rainCap();
  }, 100);
}
setInterval(() => {
  arr.value.forEach((el) => {
    el.top++;
  });
}, 0.0001);
rainCap();
</script>
<style scoped lang="scss">
.rain {
  width: 100vw;
  height: 100vh;
  background: #000;
  background: url("./assets/img/layer-1.jpg") no-repeat center / cover;
  position: absolute;
  left: 0;
  top: 0;
  &__item {
    position: fixed;
    img {
      width: 5px;
      height: 5px;
    }
  }
}
</style>
