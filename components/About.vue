<template>
  <section id="about" class="min-h-screen w-screen">
    <div class="relative mb-8 mt-36 flex flex-col items-center gap-5">
      <h2 class="font-general text-sm uppercase md:text-[10px]">
        Welcome to zentry
      </h2>

      <AnimatedTitle 
        title="Disc<b>o</b>ver the world's<br />l<b>a</b>rgest shared adventure" container-class="mt-5 !text-black text-center" 
      />

      <div class="about-subtext ">
        <p>The game of games begins—your life, now an epic MMORPG</p>
        <p class="text-gray-600">Zentry unified play layer driving attention and contribution through cross-world AI gamification.</p>
      </div>
    </div>

    <div class="h-dvh w-screen relative" id="clip">
      <NuxtImg
        src="/img/stones.webp"
        alt="about section floating stones"
        class="absolute scale-[1.2] z-40 left-0 h-full -top-20 size-full object-cover"
        loading="lazy"
      />
      <div class="mask-clip-path about-image border border-black ">
        <NuxtImg
          src="/img/about.webp"
          alt="about section background"
          class="absolute left-0 top-0 size-full object-cover"
          width="3200"
          height="1800"
        />
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  const clipAnimation = gsap.timeline({
    scrollTrigger: {
      trigger: '#clip',
      start: 'center center',
      end: '+=800 center',
      scrub: 0.5,
      pin: true,
      pinSpacing: true,
    },
  })

  clipAnimation.to('.mask-clip-path', {
    width: '100vw',
    height: '100vh',
    borderRadius: 0,
    rotateX: 0,
    rotateY: 0,
    rotateZ: 0,
  })
})
</script>

<style scoped>
  
</style>
