<template>
  <section class="min-h-dvh w-screen bg-black text-blue-50">
    <div class="flex size-full flex-col items-center py-10 pb-24">
      <p class="font-general text-sm uppercase md:text-[10px]">
        the multiversal ip world
      </p>

      <div class="relative size-full">
        <AnimatedTitle
          title="the st<b>o</b>ry of <br /> a hidden real<b>m</b>"
          container-class="mt-5 pointer-events-none mix-blend-difference relative z-10"
          text-class="text-blue-50 mix-blind-difference"
        />

        <div class="story-img-container">
          <div class="story-img-mask" ref="maskRef">
            <div class="story-img-content">
              <img
                ref="imgRef"
                @mousemove="handleMouseMove"
                @mouseleave="resetRotation"
                @mouseup="resetRotation"
                @mouseenter="resetRotation"
                src="/img/entrance.webp"
                alt="entrance.webp"
                class="object-contain"
              />
            </div>
          </div>

          <!-- rounded corner SVG -->
          <svg class="invisible absolute size-0" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <filter id="flt_tag">
                <feGaussianBlur in="SourceGraphic" stdDeviation="8" result="blur" />
                <feColorMatrix
                  in="blur"
                  mode="matrix"
                  values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -9"
                  result="flt_tag"
                />
                <feComposite in="SourceGraphic" in2="flt_tag" operator="atop" />
              </filter>
            </defs>
          </svg>
        </div>
      </div>

      <div class="-mt-44 max-sm:-mt-66 flex w-full justify-center md:-mt-64 md:me-44 md:justify-end">
        <div class="flex h-full w-fit flex-col items-center md:items-start">
          <p class="mt-3 max-w-sm text-center font-circular-web text-violet-50 md:text-start">
            Where realms converge, lies Zentry and the boundless pillar. Discover its secrets
            and shape your fate amidst infinite opportunities.
          </p>

          <NuxtLink to="/">
            <Button
              id="realm-btn"
              title="discover prologue"
              container-class="mt-5"
            />
          </NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import gsap from 'gsap'

const imgRef = ref<HTMLElement | null>(null)
const maskRef = ref<HTMLElement | null>(null)

function handleMouseMove(e: MouseEvent) {
  const element = imgRef.value
  if (!element) return

  const rect = element.getBoundingClientRect()
  const xPos = e.clientX - rect.left
  const yPos = e.clientY - rect.top

  const centerX = rect.width / 2
  const centerY = rect.height / 2

  const rotateX = ((yPos - centerY) / centerY) * -10
  const rotateY = ((xPos - centerX) / centerX) * 10

  gsap.to(element, {
    duration: 0.3,
    rotateX,
    rotateY,
    transformPerspective: 1000,
    ease: 'power1.inOut',
  })
}

function resetRotation() {
  const element = imgRef.value
  if (!element) return

  gsap.to(element, {
    duration: 0.3,
    rotateX: 0,
    rotateY: 0,
    ease: 'power1.inOut',
  })
}

function updateClipPath() {
  const el = maskRef.value
  if (!el) return

  const isMD = window.innerWidth <= 768

  gsap.to(el, {
    clipPath: isMD
      ? 'polygon(17% 0, 71% 11%, 91% 100%, 28% 100%)'
      : '',
    scale: isMD ? 1.3 : 1,
    duration: 0.5,
    ease: 'power2.inOut',
  })
}

onMounted(() => {
  updateClipPath()
  window.addEventListener('resize', updateClipPath)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateClipPath)
})
</script>

<style scoped>

</style>
