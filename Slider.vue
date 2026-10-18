<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  slides: { type: Array, default: () => [] }
})

const index = ref(0)
const total = computed(() => props.slides.length)

const prev = () => (index.value = (index.value - 1 + total.value) % total.value)
const next = () => (index.value = (index.value + 1) % total.value)
const goTo = (i) => (index.value = i)
</script>

<template>
  <div class="slider">
    <div class="slide" :style="{ background: slides[index].color }">
      {{ slides[index].text }}
    </div>
    <button class="nav prev" @click="prev">‹</button>
    <button class="nav next" @click="next">›</button>
    <div class="dots">
      <span
        v-for="(_, i) in slides"
        :key="i"
        :class="['dot', { active: i === index }]"
        @click="goTo(i)"
      />
    </div>
  </div>
</template>

<style scoped>
.slider {
  position: relative;
  max-width: 600px;
  margin: 40px auto;
  user-select: none;
}
.slide {
  width: 100%;
  height: 360px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 32px;
  font-weight: bold;
  transition: background 0.3s;
}
.nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: #fff;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
}
.nav:hover { background: rgba(0, 0, 0, 0.75); }
.prev { left: 10px; }
.next { right: 10px; }
.dots {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-top: 12px;
}
.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: #ccc;
  cursor: pointer;
  transition: background 0.2s;
}
.dot.active { background: #333; }
</style>