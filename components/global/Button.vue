<template>
  <button 
    :id="id" 
    :class="containerClass"
    class="group relative z-10 w-fit cursor-pointer overflow-hidden rounded-full bg-violet-50 px-7 py-3 text-black flex flex-row items-center justify-center gap-2"
  >
    <Icon 
      v-if="leftIcon"
      :name="leftIcon"
      :style="{ transform: `rotate(${props.iconRotation})` }"
      size="16"
      />
      <span class="relative inline-flex overflow-x font-general text-xs uppercase">
        {{ title }}
      </span>
      <Icon 
      v-if="rightIcon"
      :name="rightIcon"
      :style="{ transform: `rotate(${props.iconRotation})` }"
      size="16"
    />
  </button>
</template>

<script lang="ts" setup>
const props = defineProps({
  id: {
    type: String,
    required: false,
  },
  title: {
    type: String,
    required: true,
  },
  leftIcon: {
    type: String,
    required: false,
  },
  rightIcon: {
    type: String,
    required: false,
  },
  iconRotation: {
    type: String,
    default: '45deg',
  },
  containerClass: {
    type: String,
    default: '',
  },
});
</script>

<style>

</style>