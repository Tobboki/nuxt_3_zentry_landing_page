<template>
  <div 
    ref="headerContainerRef"
    :class="containerClass"
  >
    <header class="absolute top-1/2 w-full -translate-y-1/2">
      <nav class="flex size-full items-center justify-between p-4">
        <div class="flex items-center gap-3">
          <NuxtLink to="/">
            <NuxtImg 
              :src="isSecondaryTheme 
                ? '/img/Zentry Logo/zentry-symbol-black.png'
                : '/img/Zentry Logo/zentry-symbol-white.png'"
              alt="zentry logo"
              width="64"
              height="64"
            />
          </NuxtLink>

          <div class="flex flex-nowrap gap-2">
            <Button 
              id="product-button"
              title="Products"
              rightIcon="fluent:location-arrow-24-filled"
              :container-class="buttonClass"
              icon-rotation="135deg"
            />
            <Button 
              id="whitepaper-button"
              title="Whitepaper"
              :container-class="buttonClass"
              icon-rotation="135deg"
            />
          </div>
        </div>

        <ul class="flex h-full items-center gap-2">
          <li 
            v-for="(item, index) in navItems" 
            :key="index"
            :class="navItemClass"
          >
            <NuxtLink :to="item.link">
              {{ item.name }}
            </NuxtLink>
          </li>

          <li 
            class="ms-4 p-2 cursor-pointer"
            @click="playAudio ? toggleAudioIndicator() : null"
          >
            <button class="flex items-center space-x-0.5 cursor-pointer" type="button" aria-label="Toggle music">
              <audio
                ref="audioElementRef" 
                src="/audio/loop.mp3"
                class="hidden"
                loop
              ></audio>
              <div 
                v-for="bar in [1, 2, 3, 4]"
                :key="bar"
                class="indicator-line"
                :class="{
                  'active': isIndicatorActive && playAudio,
                  'secondary': isSecondaryTheme
                }"
                :style="{ animationDelay: `${bar * 0.2}s` }"
              ></div>
            </button>
          </li>
        </ul>
      </nav>
    </header>
  </div>
</template>

<script lang="ts" setup>
import { computed, ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useWindowScroll } from '@vueuse/core'
import gsap from 'gsap'

const props = defineProps({
  theme: {
    type: String as PropType<'primary' | 'secondary'>,
    default: 'primary'
  },
  playAudio: {
    type: Boolean,
    default: true
  }
})

const isSecondaryTheme = computed(() => props.theme === 'secondary')

const navItems = [
  { name:'Nexus', link: '' },
  { name:'Vault', link: '' },
  { name:'Prologue', link: '' },
  { name:'About', link: '#about' },
  { name:'Contact', link: '' },
]

const isAudioPlaying = ref(false)
const isIndicatorActive = ref(false)

const audioElementRef = ref<HTMLAudioElement | null>(null)
const headerContainerRef = ref<HTMLElement | null>(null)

const isNavVisible = ref(true)
const lastScrollY = ref(0)
const { y: currentScrollY } = useWindowScroll()

watch([currentScrollY], ([newY]) => {
  if (!headerContainerRef.value) return

  if (newY === 0) {
    isNavVisible.value = true
    headerContainerRef.value.classList.remove('floating-nav')
  } else if (newY > lastScrollY.value) {
    isNavVisible.value = false
    headerContainerRef.value.classList.add('floating-nav')
  } else if (newY < lastScrollY.value) {
    isNavVisible.value = true
    headerContainerRef.value.classList.add('floating-nav')
  }

  lastScrollY.value = newY
})

watch(isNavVisible, (visible) => {
  if (!headerContainerRef.value) return

  gsap.to(headerContainerRef.value, {
    y: visible ? 0 : -100,
    opacity: visible ? 1 : 0,
    duration: 0.2,
    ease: 'power1.out',
  })
})

// Theme-based class maps
const containerClass = computed(() => [
  'fixed inset-x-0 top-4 z-50 h-20 border-none transition-all duration-700 sm:inset-x-6',
  { secondary: isSecondaryTheme.value }
])

const navItemClass = computed(() => [
  'nav-hover-btn hidden md:flex',
  { secondary: isSecondaryTheme.value }
])

const buttonClass = computed(() => [
  'md:flex hidden items-center justify-center gap-1',
  isSecondaryTheme.value ? '!bg-black text-blue-50' : 'bg-blue-50'
].join(' '))

// Audio fading logic
const isFading = ref(false)
let fadeIntervalId: number | null = null

const fadeAudio = (
  audio: HTMLAudioElement,
  targetVolume: number,
  duration: number
): Promise<void> => {
  if (fadeIntervalId !== null) {
    clearInterval(fadeIntervalId)
    fadeIntervalId = null
  }

  return new Promise((resolve) => {
    const stepTime = 50
    const steps = duration / stepTime
    const volumeStep = (targetVolume - audio.volume) / steps
    let currentStep = 0

    isFading.value = true

    fadeIntervalId = window.setInterval(() => {
      currentStep++
      audio.volume = Math.min(Math.max(audio.volume + volumeStep, 0), 1)

      if (currentStep >= steps) {
        clearInterval(fadeIntervalId!)
        fadeIntervalId = null
        if (targetVolume === 0) audio.pause()
        isFading.value = false
        resolve()
      }
    }, stepTime)
  })
}

const hasStartedAudioOnce = ref(false)
let shouldResumeAfterFocus = false

const toggleAudioIndicator = async () => {
  if (!props.playAudio) return
  if (isFading.value || !audioElementRef.value) return

  const audio = audioElementRef.value
  isAudioPlaying.value = !isAudioPlaying.value
  isIndicatorActive.value = !isIndicatorActive.value

  if (isAudioPlaying.value) {
    if (!hasStartedAudioOnce.value) {
      audio.currentTime = 67
      hasStartedAudioOnce.value = true
    }
    audio.volume = 0
    audio.play()
    await fadeAudio(audio, 0.2, 1000)
  } else {
    await fadeAudio(audio, 0, 1000)
  }
}

const pauseAudioOnBlur = async () => {
  if (!props.playAudio || !audioElementRef.value) return

  const audio = audioElementRef.value

  if (!audio.paused) {
    shouldResumeAfterFocus = true
    await fadeAudio(audio, 0, 500)
    audio.pause()
    isIndicatorActive.value = false
  } else {
    shouldResumeAfterFocus = false
  }
}

const resumeAudioOnFocus = async () => {
  if (!props.playAudio || !audioElementRef.value || !shouldResumeAfterFocus) return

  const audio = audioElementRef.value
  audio.volume = 0
  audio.play()
  await fadeAudio(audio, 0.2, 500)
  isIndicatorActive.value = true
  shouldResumeAfterFocus = false
}

onMounted(() => {
  if (!props.playAudio) return

  const onVisibilityChange = () => {
    if (document.hidden) pauseAudioOnBlur()
    else resumeAudioOnFocus()
  }

  document.addEventListener('visibilitychange', onVisibilityChange)
  window.addEventListener('blur', pauseAudioOnBlur)
  window.addEventListener('focus', resumeAudioOnFocus)

  onBeforeUnmount(() => {
    document.removeEventListener('visibilitychange', onVisibilityChange)
    window.removeEventListener('blur', pauseAudioOnBlur)
    window.removeEventListener('focus', resumeAudioOnFocus)
  })
})
</script>

<style>
/* Your styles here */
</style>
