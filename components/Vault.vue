<template>
  <section class="h-dvh bg-yellow-300 flex items-center justify-between px-10 py-16 sticky">
    <div class="max-w-xl h-full space-y-10 flex flex-col justify-between z-20">
      <!-- Animated Text Group -->
      <div class="flex flex-col gap-12 vault-text-group">
        <h1 class="text-[5vw] max-md:text-[3rem] leading-24 max-md:leading-12 special-font font-zentry w-full">
          THE UNIV<b>E</b>RSE <br /> POWERED BY ZE<b>N</b>T
        </h1>

        <NuxtLink to="/vault">
          <button class="bg-black text-white px-6 py-2 rounded-full font-mono text-sm tracking-wider">
            ENTER VAULT
          </button>
        </NuxtLink>
      </div>

      <!-- Steps List -->
      <ol class="w-dvw flex flex-col gap-8 snap-y snap-mandatory text-black">
        <li v-for="(section, index) in sections" :key="index" class="max-w-md">
          <div class="flex flex-col flex-nowrap gap-4">
            <header class="relative flex ps-[4rem] w-full text-sm text-gray-500 vault-item-header font-general cursor-pointer">
              <span class="absolute top-0 left-0 text-sm">{{ index + 1 < 10 ? `0${index + 1}` : index + 1 }}</span>
              <span class="uppercase leading-none text-nowrap">{{ section.title }}</span>
            </header>
            <div class="relative ps-[4rem] vault-item-content hidden opacity-0">
              <div class="vault-content-scroll-track">
                <div class="vault-content-scroll-progress-bar" />
              </div>
              <p class="p-1">{{ section.description }}</p>
            </div>
          </div>
        </li>
      </ol>
    </div>

    <!-- Video Display -->
    <div
      class="absolute bottom-0 right-0 
            w-[24vw] h-[48vh] 
            max-xl:w-88 max-xl:h-88
            max-lg:w-80 max-lg:h-80
            max-md:w-[80vw] max-md:h-[40vh] 
            max-md:left-1/2 max-md:translate-x-[-50%] max-md:translate-y-[-75%] max-md:right-auto"
    >
      <video
        v-for="(video, i) in videos"
        :key="i"
        autoplay
        loop
        muted
        playsinline
        :class="['hidden', 'w-full', 'h-full', 'object-contain', 'vault-symbol-video', { active: i === 0 }]"
        :src="video"
      />
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sections = [
  {
    title: 'Shaping Zentry Collectively',
    description: 'Participate in governance, influence key decisions in the ever-growing Zentry Universe that is limited only by people\'s imaginations.'
  },
  {
    title: 'Unlocking Economic Opportunity',
    description: 'ZENT, a commodity-based currency that unlocks exclusive benefits, airdrops, quotas, and co-creation within and beyond Zentry ecosystem.'
  },
  {
    title: 'Sharing Value Accrued',
    description: 'ZENT holders thrive as Zentry grows, benefiting from the expansive partnerships, treasury investment and economic activities.'
  }
]

const videos = [
  '/videos/vault/symbol_1.webm',
  '/videos/vault/symbol_2.webm',
  '/videos/vault/symbol_3.webm'
]

onMounted(() => {
  const headers = document.querySelectorAll('.vault-item-header')
  const contents = document.querySelectorAll('.vault-item-content')
  const videoEls = document.querySelectorAll('.vault-symbol-video')
  const bars = document.querySelectorAll('.vault-content-scroll-progress-bar')

  let activeIndex = 0

  const activate = (index) => {
    activeIndex = index

    headers.forEach(h => h.classList.remove('active'))
    contents.forEach(c => c.classList.add('hidden', 'opacity-0'))
    videoEls.forEach(v => v.classList.remove('active', 'block'))
    bars.forEach(b => b.style.height = '0%')

    headers[index].classList.add('active')
    contents[index].classList.remove('hidden', 'opacity-0')
    videoEls[index]?.classList.add('active', 'block')

    // Animate content reveal
    gsap.fromTo(contents[index], {
      y: 40,
      opacity: 0
    }, {
      y: 0,
      opacity: 1,
      duration: 0.6,
      ease: "power3.out"
    })

    // Animate video entrance
    gsap.fromTo(videoEls[index], {
      x: 100,
      y: 100,
      opacity: 0
    }, {
      x: 0,
      y: 0,
      opacity: 1,
      duration: 1,
      ease: "power4.out"
    })

    // Progress bar
    gsap.to(bars[index], {
      height: '100%',
      duration: 0.3,
      ease: 'power1.out'
    })
  }

  activate(0)

  headers.forEach((header, i) => {
    header.addEventListener('click', () => {
      if (i !== activeIndex) activate(i)
    })
  })

  const ctx = gsap.context(() => {
    // Animate the full vault text group (heading + button)
    gsap.from(".vault-text-group", {
      y: -120,
      opacity: 0,
      duration: 1.3,
      ease: "power4.out",
      scrollTrigger: {
        trigger: ".vault-text-group",
        start: "top 90%",
        toggleActions: "play none none reverse"
      }
    })

    // Animate each vault step from the side
    document.querySelectorAll("ol li").forEach((el, index) => {
      gsap.from(el, {
        x: -150,
        opacity: 0,
        duration: 1.3,
        ease: "power4.out",
        scrollTrigger: {
          trigger: el,
          start: "top 100%",
          toggleActions: "play none none reverse",
        }
      })
    })

    // Animate the first active video
    gsap.fromTo(".vault-symbol-video.active", {
      y: 100,
      opacity: 0
    }, {
      scrollTrigger: {
        trigger: ".vault-symbol-video.active",
        start: "top 85%",
        end: "bottom 100%",
        toggleActions: "play none none reverse"
      },
      y: 0,
      opacity: 1,
      duration: 1.3,
      ease: "power3.out"
    })
  })

  onBeforeUnmount(() => {
    ctx.revert()
    headers.forEach((header, i) => {
      header.removeEventListener('click', () => activate(i))
    })
  })
})
</script>

<style scoped>

</style>
