<template>
  <article
    ref="cardRef"
    class="relative rounded-md overflow-hidden border-hsla size-full transition-all duration-100 ease-in-out will-change-transform cursor-pointer"
    @mousemove="handleMouseMove"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
    :style="{ transform: transformStyle }"
  >
    <video 
      ref="videoRef"
      :src="src"
      loop
      muted
      class="absolute left-0 top-0 size-full object-cover object-center"
    />
    <div class="relative z-10 flex size-full flex-col justify-between p-5 text-blue-50">
      <div>
        <h1 class="bento-title special-font" v-html="title" />
        <p v-if="description" class="mt-3 max-w-64 text-xs md:text-base">
          {{ description }}
        </p>
      </div>

      <div class="flex gap-2">
        <Button 
          v-if="isComingSoon"
          title="Coming soon"
          container-class="!bg-black border text-blue-50 opacity-50"
          left-icon="typcn:location-arrow"
          icon-rotation="0deg"
        />
        
        <Button 
          v-if="isLaunchReady"
          title="Launch site"
          container-class="!bg-black border !border-yellow-200 text-yellow-300"
          right-icon="typcn:location-arrow"
          icon-rotation="0deg"
        />
      </div>
    </div>
  </article>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const props = defineProps({
  src: { type: String, required: true },
  title: { type: String, required: true },
  description: { type: String, required: false },
  isComingSoon: { type: Boolean, default: false },
  isLaunchReady: { type: Boolean, default: false },
})

const cardRef = ref<HTMLElement | null>(null)
const videoRef = ref<HTMLVideoElement | null>(null)
const transformStyle = ref('')

const handleMouseMove = (event: MouseEvent) => {
  if (!cardRef.value) return

  const { left, top, width, height } = cardRef.value.getBoundingClientRect()
  const relativeX = (event.clientX - left) / width
  const relativeY = (event.clientY - top) / height

  const tiltX = (relativeY - 0.5) * 10
  const tiltY = (relativeX - 0.5) * -10

  transformStyle.value = `perspective(1000px) rotateX(${tiltX}deg) rotateY(${tiltY}deg) scale3d(.95, .95, .95)`
}

const handleMouseEnter = () => {
  transformStyle.value = ''
  videoRef.value?.play()
}

const handleMouseLeave = () => {
  transformStyle.value = ''
  if (videoRef.value) {
    videoRef.value.pause()
    videoRef.value.currentTime = 0
  }
}
</script>


<style>

</style>