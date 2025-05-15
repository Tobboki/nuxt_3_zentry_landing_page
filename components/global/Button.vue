<template>
  <button 
    :id="id" 
    :class="containerClass"
    class="group relative z-10 w-fit cursor-pointer overflow-hidden rounded-full bg-violet-50 px-7 py-3 text-black"
  >
    <Icon 
      :name="leftIcon"
      class=" rotate-45"
    />
    <span class="relative inline-flex overflow-x font-general text-xs uppercase">
      {{ title }}
    </span>
  </button>
</template>

<script lang="ts" setup>
defineProps({
  id: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  leftIcon: {
    type: String,
    required: false,
  },
  containerClass: {
    type: String,
    default: '',
  },
})
</script>

<style>

</style>