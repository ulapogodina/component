<script setup>
import Slider from './Slider.vue'

const slides = [
  { color: '#e74c3c', text: 'Слайд 1' },
  { color: '#3498db', text: 'Слайд 2' },
  { color: '#2ecc71', text: 'Слайд 3' },
  { color: '#f39c12', text: 'Слайд 4' }
]
</script>

<template>
  <Slider :slides="slides" />
</template>