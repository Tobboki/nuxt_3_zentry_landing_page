<template>
  <footer class="w-screen bg-violet-300 py-4 text-black">
    <!-- Zentry Text Logo -->
    <div class="w-full bg-violet-300">
      <h1 class="special-font leading-[32vw] font-zentry will-change-transform text-center uppercase text-[36vw] select-none">
        Zentr<b>y</b>
      </h1>
    </div>

    <!-- Grid Layout -->
    <div class="flex flex-row max-md:flex-col justify-center items-center flex-nowrap w-full">
      <NuxtImg
        src="/img/Zentry Logo/zentry-symbol-black.png"
        class="w-36 select-none"
      />

      <div
        class="grid grid-cols-4 grid-rows-1 max-md:grid-cols-2 max-md:grid-rows-2 max-sm:grid-cols-1 max-sm:grid-rows-4 max-md:text-center items-start content-center w-full mx-auto p-5 gap-y-6"
      >
        <nav
          v-for="(section, index) in footerSections"
          :key="index"
        >
          <h1
            class="font-robert-medium uppercase mb-5 cursor-pointer gap-2 select-none transition-colors duration-200 hover:text-yellow-300"
            @click="toggleSection(index)"
          >
            <span class="text-lg sm:text-xl">
              {{ section.title }}
              <span class="sm:hidden text-yellow-300 ml-2 transition-transform duration-200">
                {{ section.isOpen ? '-' : '+' }}
              </span>
            </span>
          </h1>


          <ul
            class="font-robert-medium text-2xl transition-all duration-300 ease-in-out sm:block max-sm:overflow-hidden max-sm:transition-all max-sm:duration-300 max-sm:max-h-0"
            :class="{ 'max-sm:max-h-96': section.isOpen }"
          >
            <li
              v-for="(link, idx) in section.links"
              :key="idx"
            >
              <NuxtLink :to="link.link" class="text-nowrap">
                {{ link.title }}
              </NuxtLink>
            </li>
          </ul>
        </nav>
      </div>
    </div>

    <!-- Bottom Footer -->
    <div class="container mx-auto flex flex-col items-center justify-between gap-4 px-4 md:flex-row">
      <p class="text-center text-sm font-light md:text-left">
        ©Tobboki 2024. All rights reserved
      </p>

      <a
        href="#privacy-policy"
        class="text-center text-sm font-light md:text-right"
      >
        Privacy Policy
      </a>
    </div>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const footerSections = ref([
  {
    title: 'Explore',
    isOpen: false,
    links: [
      { title: 'Home', link: '/' },
      { title: 'Prologue', link: '/prologue' },
      { title: 'About', link: '/about' },
      { title: 'Contact', link: '/contact' },
    ]
  },
  {
    title: 'Products',
    isOpen: false,
    links: [
      { title: 'Radiant', link: '/radiant' },
      { title: 'Nexus', link: '/nexus' },
      { title: 'Zigma', link: '/zigma' },
      { title: 'Azul', link: '/azul' },
    ]
  },
  {
    title: 'Follow Us',
    isOpen: false,
    links: [
      { title: 'discord', link: '/' },
      { title: 'x', link: '/' },
      { title: 'youtube', link: '/' },
      { title: 'medium', link: '/' },
    ]
  },
  {
    title: 'Resources',
    isOpen: false,
    links: [
      { title: 'Media Kit', link: '/' }
    ]
  },
])

const toggleSection = (index) => {
  footerSections.value[index].isOpen = !footerSections.value[index].isOpen
}
</script>
