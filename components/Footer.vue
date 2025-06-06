<template>
  <footer class="w-screen bg-violet-300 py-4 text-black">
    <!-- Zentry Text Logo -->
    <div class="w-full">
      <h1 class="special-font leading-[32vw] font-zentry will-change-transform text-center uppercase text-[36vw] select-none">
        Zentr<b>y</b>
      </h1>
    </div>

    <!-- Grid Layout -->
    <div class="flex flex-row max-md:flex-col justify-center items-center w-full">
      <NuxtImg
        src="/img/Zentry Logo/zentry-symbol-black.png"
        class="w-36 select-none"
      />

      <div
        class="grid grid-cols-4 max-md:grid-cols-2 max-md:grid-rows-2 max-sm:flex max-sm:flex-col text-center w-full mx-auto p-5 gap-y-6"
      >
        <nav
          v-for="(section, index) in footerSections"
          :key="index"
        >
          <!-- Section Header -->
          <h2
            class="font-robert-medium uppercase mb-5 cursor-pointer gap-2 select-none transition-colors duration-200 hover:text-yellow-300"
            @click="toggleSection(index)"
            role="button"
            :aria-expanded="openSectionIndex === index"
          >
            <span class="text-lg sm:text-xl">
              {{ section.title }}
              <span class="sm:hidden text-yellow-300 ml-2 transition-transform duration-200">
                {{ openSectionIndex === index ? '−' : '+' }}
              </span>
            </span>
          </h2>

          <!-- Section Links -->
          <ul
            class="font-robert-medium text-2xl transition-all duration-300 ease-in-out sm:block overflow-hidden"
            :class="{
              'max-sm:max-h-96': openSectionIndex === index,
              'max-sm:max-h-0': openSectionIndex !== index
            }"
          >
            <li
              v-for="(link, idx) in section.links"
              :key="idx"
              class="mb-2"
            >
              <NuxtLink 
                :to="link.disabled ? '' : link.link" 
                class="text-nowrap select-none inline-flex items-center gap-1"
                :class="{
                  'text-muted text-gray-900 cursor-default pointer-events-none': link.disabled,
                  'hover:text-yellow-600 transition-colors duration-200': !link.disabled
                }"
                :aria-disabled="link.disabled"
              >
                {{ link.title }}
                <Icon 
                  v-if="link.icon"
                  :name="link.icon"
                />
              </NuxtLink>
            </li>
          </ul>
        </nav>
      </div>
    </div>

    <!-- Bottom Footer -->
    <div class="container mx-auto flex flex-col items-center justify-between gap-4 px-4 md:flex-row">
      <p class="text-center text-sm font-light md:text-left">
        © Tobboki 2024. All rights reserved.
      </p>

      <a
        href="#privacy-policy"
        class="text-center text-sm font-light md:text-right hover:underline"
      >
        Privacy Policy
      </a>
    </div>
  </footer>
</template>

<script setup>
const openSectionIndex = ref(null)

const footerSections = reactive([
  {
    title: 'Explore',
    links: [
      { title: 'Home', link: '/', disabled: false },
      { title: 'Prologue', link: '/prologue', disabled: false },
      { title: 'About', link: '/about', disabled: false },
      { title: 'Contact', link: '/contact', disabled: false },
    ]
  },
  {
    title: 'Products',
    links: [
      { title: 'Radiant', link: '/radiant', icon: 'uis:arrow-up-right', disabled: true },
      { title: 'Nexus', link: '/nexus', icon: 'uis:arrow-up-right', disabled: false },
      { title: 'Zigma', link: '/zigma', icon: 'uis:arrow-up-right', disabled: true },
      { title: 'Azul', link: '/azul', icon: 'uis:arrow-up-right', disabled: true },
    ]
  },
  {
    title: 'Follow Us',
    links: [
      { title: 'discord', link: '/', disabled: false },
      { title: 'x', link: '/', disabled: false },
      { title: 'youtube', link: '/', disabled: false },
      { title: 'medium', link: '/', disabled: false },
    ]
  },
  {
    title: 'Resources',
    links: [
      { title: 'Media Kit', link: '/', disabled: false }
    ]
  },
])

// Toggle section open/closed
const toggleSection = (index) => {
  openSectionIndex.value = openSectionIndex.value === index ? null : index
}
</script>

<style>

</style>