<template>
  <div ref="containerRef" :class="['animated-title font-zentry', containerClass]">
    <div
      v-for="(line, index) in lines"
      :key="index"
      class="flex-center max-w-full flex-wrap gap-2 px-10 md:gap-3"
    >
      <span
        v-for="(word, idx) in splitLine(line)"
        :key="idx"
        class="animated-word"
        v-html="word"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, onBeforeUnmount, computed } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

interface Props {
  title: string;
  containerClass?: string;
}

const props = defineProps<Props>();

const containerRef = ref<HTMLElement | null>(null);

const lines = computed(() => props.title.split('<br />'));

const splitLine = (line: string) => line.split(' ');

onMounted(() => {
  if (!containerRef.value) {
    console.error('containerRef is not defined');
    return;
  }

  const ctx = gsap.context((self) => {
    // Select .animated-word elements within the containerRef scope
    const words = self.selector!('.animated-word');

    const timeline = gsap.timeline({
      scrollTrigger: {
        trigger: containerRef.value,
        start: '100 bottom', // Adjusted to ensure visibility
        end: 'center bottom',
        toggleActions: 'play none none reverse',
      },
    });

    timeline.to(words, {
      opacity: 1,
      transform: 'translate3d(0, 0, 0) rotateY(0deg) rotateX(0deg)',
      ease: 'power2.inOut',
      stagger: 0.02,
      duration: 1
    });
  }, containerRef.value); // Pass containerRef.value directly

  // Cleanup on unmount
  onBeforeUnmount(() => {
    ctx.revert();
  });
});
</script>

<style scoped>
/* Scoped styles are empty, but you can add any component-specific styles here */
</style>