<script setup>
import { onMounted } from "vue";

import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: "#hero",
      start: "top top",
      end: "bottom top",
      scrub: true,
    },
  });

  gsap.utils.toArray(".parallax").forEach((layer) => {
    const depth = layer.dataset.depth;
    const movement = -(layer.offsetHeight * depth);
    tl.to(layer, { y: movement, ease: "none" }, 0);
  });
});
</script>

<template>
  <div id="hero">
    <h1 class="header parallax" data-depth="0.10">Los Angeles <span>Mountains</span></h1>

    <div class="layer-bg layer parallax" data-depth="0.10"></div>
    <div class="layer-1 layer parallax" data-depth="0.30"></div>
    <div class="layer-2 layer parallax" data-depth="0.20"></div>
    <div class="layer-overlay layer parallax" data-depth="0.50"></div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");

#hero {
  height: 100vh;
  max-width: 100%;
  overflow: hidden;
  position: relative;
  margin: 0 auto;
}

.header {
  font-family: "Bebas Neue", sans-serif;
  font-weight: 400;
  font-style: normal;
  position: fixed;
  top: 20%;
  left: 20%;
  color: #4d4d4d;
  z-index: 1;
  font-size: 160px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  line-height: 0.8;
}

.header span {
  font-size: 180px;
  background: -webkit-linear-gradient(#414f6b, #000);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.layer {
  background-position: bottom center;
  background-size: contain;
  background-repeat: no-repeat;
  width: 100%;
  height: 100vh;
  position: fixed;
  object-fit: cover;
}

.layer-bg {
  background-image: url("/background/hero-background.jpg");
  background-size: cover;
}
.layer-1 {
  background-image: url("/background/mountain-right.png");
  background-position: right bottom;
  z-index: 4;
}
.layer-2 {
  background-image: url("/background/mountain-left.png");
  background-position: left bottom;
  z-index: 2;
}
.layer-overlay {
  background-image: url("/background/overlay.png");
  background-size: cover;
  z-index: 6;
  opacity: 10%;
}
</style>
