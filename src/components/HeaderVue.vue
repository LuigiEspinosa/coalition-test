<script setup>
import { ref, onMounted, onBeforeUnmount, computed } from "vue";

const isScrolled = ref(false);
const textColor = computed(() => (isScrolled.value ? "#414f6b" : "white"));

const handleScroll = () => {
  isScrolled.value = window.scrollY > 0;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <header
    class="fixed w-full top-0 bg-transparent transition-all duration-300 ease-in-out z-50"
    :class="{ 'bg-[#fff] shadow-lg': isScrolled }"
  >
    <div class="container mx-auto flex items-center justify-between py-4">
      <div class="flex items-center justify-between w-full">
        <img src="/logo.svg" alt="Logo" class="h-[43px]" />

        <div class="header-menu ml-4 space-x-4">
          <a
            href="#"
            class="font-bold italic text-xs leading-5 uppercase text-white transition border-b-white border-b border-solid"
            :style="{ color: textColor }"
            >01. History</a
          >
          <a
            href="#"
            class="font-bold italic text-xs leading-5 uppercase text-white transition border-b-white border-b border-solid"
            :style="{ color: textColor }"
            >02. Team</a
          >
        </div>
      </div>
    </div>
  </header>
</template>
