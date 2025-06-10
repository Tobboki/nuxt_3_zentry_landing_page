<template>
  <section class="w-screen">
    <div class="my-36 flex flex-col items-center gap-6">
      <h2 class="font-general text-sm uppercase md:text-[10px]">who we are</h2>

      <p
        class="text-[8vw] leading-[14vh] max-xl:leading-[10vh] max-lg:leading-[8vh] max-md:leading-[6vh] max-sm:leading-[4vh] uppercase special-font font-zentry flex flex-col items-center justify-center"
      >
        <span>we're b<b>u</b>ilding</span>

        <span class="flex items-center">
          <span>a new</span>
          <span ref="square1" class="discover-square relative overflow-hidden">
            <img
              ref="img1"
              class="absolute inset-0 w-full h-full object-cover opacity-0 scale-125 pointer-events-none"
              :src="imageUrls[0]"
              alt="Discover Image 1"
            />
          </span>
          <span>realit<b>y</b></span>
        </span>

        <span>that rew<b>a</b>rds</span>

        <span class="flex items-center">
          <span>play<b>e</b>rs</span>
          <span ref="square2" class="discover-square relative overflow-hidden">
            <img
              ref="img2"
              class="absolute inset-0 w-full h-full object-cover opacity-0 scale-125 pointer-events-none"
              :src="imageUrls[1]"
              alt="Discover Image 2"
            />
          </span>
          <span>and</span>
        </span>

        <span>e<b>m</b>powers</span>

        <span>hu<b>m</b>ans & AI</span>

        <span class="flex items-center">
          <span>to</span>
          <span ref="square3" class="discover-square relative overflow-hidden">
            <img
              ref="img3"
              class="absolute inset-0 w-full h-full object-cover opacity-0 scale-125 pointer-events-none"
              :src="imageUrls[2]"
              alt="Discover Image 3"
            />
          </span>
          <span>thri<b>v</b>e</span>
        </span>
      </p>

      <p class="flex flex-col font-circular-web text-center">
        <span>Zentry envisions a future where players, emerging tech, and</span>
        <span>a new economy unite at the convergence of gaming and AI.</span>
      </p>

      <NuxtLink to="/">
        <Button title="Discover who we are" container-class="!bg-black text-blue-50 font-bold" />
      </NuxtLink>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import gsap from 'gsap'

const square1 = ref<HTMLElement | null>(null)
const square2 = ref<HTMLElement | null>(null)
const square3 = ref<HTMLElement | null>(null)

const img1 = ref<HTMLImageElement | null>(null)
const img2 = ref<HTMLImageElement | null>(null)
const img3 = ref<HTMLImageElement | null>(null)

const imageUrls = [
  '/img/discover/About_Entry_Visuals_01.webp',
  '/img/discover/About_Entry_Visuals_02.webp',
  '/img/discover/About_Entry_Visuals_03.webp'
]

const squares = [square1, square2, square3]
const imgs = [img1, img2, img3]

onMounted(() => {
  squares.forEach((squareRef, i) => {
    const square = squareRef.value
    const img = imgs[i].value

    if (!square || !img) return

    square.addEventListener('mouseenter', () => {
      gsap.to(img, {
        opacity: 1,
        scale: 1,
        duration: 1,
        ease: 'power3.out'
      })

      gsap.to(square, {
        padding: 4,
        scaleX: 6,
        scaleY: 4,
        duration: 1,
        ease: 'power3.out',
        background: 'transparent'
      })
    })

    square.addEventListener('mouseleave', () => {
      gsap.to(img, {
        opacity: 0,
        scale: 1.25,
        duration: 1,
        ease: 'power3.inOut'
      })

      gsap.to(square, {
        scaleX: 1,
        scaleY: 1,
        duration: 1,
        ease: 'power3.inOut',
        backgroundColor: '#000'
      })
    })

    square.addEventListener('mousemove', (e: MouseEvent) => {
      const rect = square.getBoundingClientRect()
      const x = e.clientX - rect.left
      const y = e.clientY - rect.top

      const centerX = rect.width / 2
      const centerY = rect.height / 2

      const rotateX = ((y - centerY) / centerY) * -20
      const rotateY = ((x - centerX) / centerX) * 20

      gsap.to(img, {
        duration: 0.2,
        rotateX,
        rotateY,
        transformPerspective: 1000,
        ease: 'power1.inOut',
      })
    })
  })
})
</script>

<style scoped>

</style>
