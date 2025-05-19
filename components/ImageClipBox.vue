<template>
  <div :class="clipClass">
    <img 
      :src="src" 
      :alt="alt || 'decorative image'" 
      class="w-full h-full object-cover"
      loading="lazy"
    />
  </div>
</template>

<script setup>
defineProps({
  src: {
    type: String,
    required: true
  },
  clipClass: {
    type: String,
    default: ''
  },
  alt: {
    type: String,
    default: ''
  }
})
</script>

<style>
  
</style>