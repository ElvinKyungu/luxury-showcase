<script setup>
import { ref, onMounted } from "vue"
import { animate } from "motion"

const hoverTexts = ref(["F/W 2025", "S/S 2026", "A/W 202700000000000"])

const hoverContainer = ref(null)
const borderMover = ref(null)

const activeIndex = ref(null)

const moveBorder = (index) => {
  const items = hoverContainer.value.querySelectorAll(".hover-item")
  const target = items[index]

  if (!target) return

  const { top, left, width, height } = target.getBoundingClientRect()
  const containerOffset = hoverContainer.value.getBoundingClientRect()

  animate(borderMover.value, {
    top: `${top - containerOffset.top}px`,
    left: `${left - containerOffset.left}px`,
    width: `${width}px`,
    height: `${height}px`,
  })

  activeIndex.value = index
}

onMounted(() => {
  moveBorder(0)
})
</script>


<template>
  <div class="relative flex items-center justify-center h-screen bg-black text-white">
    <div class="text-center">
      <p class="text-gray-400 font-serif text-2xl">Prestige</p>
      <p class="text-gray-400 font-serif text-2xl mt-2">S/S 2024</p>

      <div ref="hoverContainer" class="relative mt-6 grid">
        <span ref="borderMover" class="corner-border"></span>
        <div
          v-for="(text, index) in hoverTexts"
          :key="index"
          class="hover-item relative font-serif font-semibold cursor-pointer text-3xl text-gray-400 mt-2 px-4 py-2"
          @mouseover="moveBorder(index)"
          :class="{ active: activeIndex === index }"
        >
          {{ text }}
        </div>
      </div>

      <p class="text-gray-400 font-serif text-2xl mt-6">Previously Loved</p>
      <p class="text-gray-400 font-serif text-2xl mt-2">Black Friday</p>
    </div>

    <footer class="absolute bottom-4 text-center text-gray-300 text-sm">
      "Unearthed. Unrivaled."
    </footer>
  </div>
</template>


<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600&display=swap');

body {
  font-family: 'Playfair Display', serif;
}

.hover-item {
  z-index: 1;
  transition: color 0.3s ease;
}

.hover-item.active {
  color: #ffffff;
}
.corner-border {
  position: relative;
  display: inline-block;
  padding: 10px;
}

.corner-border::before,
.corner-border::after,
.corner-border .corner-top-right,
.corner-border .corner-bottom-left {
  content: '';
  position: absolute;
  border: 2px solid #3b82f6;
  width: 10px;
  height: 10px;
}

.corner-border::before {
  top: -2px;
  left: -2px;
  border-right: none;
  border-bottom: none;
}

.corner-border::after {
  bottom: -2px;
  right: -2px;
  border-left: none;
  border-top: none;
}

.corner-border .corner-top-right {
  top: -2px;
  right: -2px;
  border-left: none;
  border-bottom: none;
}

.corner-border .corner-bottom-left {
  bottom: -2px;
  left: -2px;
  border-right: none;
  border-top: none;
}
</style>
