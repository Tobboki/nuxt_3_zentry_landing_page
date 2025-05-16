<template>
  <section class="relative h-dvh w-screen overflow-x-hidden bg">
    <div 
      id="video-frame" 
      class="relative z-10 h-dvh w-screen overflow-hidden rounded-lg bg-blue-75"
    >
        <div>
          <div 
            class="mask-clip-path absolute-center absolute z-50 size-64 cursor-pointer overflow-hidden rounded-lg" 
            >
            <div 
              class="origin-center scale-50 opacity-0 transition-all duration-500 ease-in hover:scale-100 hover:opacity-100"
              @click="handleMiniVideoClick"
            >
              <video 
                id="current-video"
                ref="currentVideoRef"
                loop
                muted
                :src="getVideoSrc(currentIndex + 1)"
                class="size-64 origin-center scale-150 object-cover object-center"
                @loadeddata="handleVideoLoad"
              />
            </div>
          </div>

          <video 
            ref="nextVideoRef"
            id="next-video"
            loop
            muted
            :src="getVideoSrc(currentIndex)"
            class="absolute-center invisible absolute z-20 size-64 object-cover object-center"
            @loadeddata="handleVideoLoad"
          />

          <video 
            :src="getVideoSrc((currentIndex === totalVideosNumber-1) ? 1 : currentIndex)" 
            autoplay
            loop
            muted
            class="absolute left-0 top-0 size-full object-cover object-center"
            @loadeddata="handleVideoLoad"
          />
        </div>

        <h1
          class="special-font hero-heading absolute bottom-5 right-5 z-40 text-blue-75"
        >
          G<b>a</b>ming
        </h1>

        <div class="absolute top-0 left-0 z-40 size-full">
          <div class="mt-24 px-5 sm:px-10">
            <h1 class="special-font hero-heading text-blue-100">
              redfi<b>n</b>e
            </h1>

            <p class="mb-5 max-w-64 font-robert-regular text-blue-100">
              Enter the meta game Layer <br> Unleash the Play Economy
            </p>
            <Button
              id="watch-trailer"
              title="Watch Trailer"
              leftIcon="fluent:location-arrow-24-filled"
              containerClass="bg-yellow-300 flex-center gap-2"
            />
          </div>
        </div>
    </div>
    <h1 class="special-font hero-heading absolute bottom-5 right-5 text-black">
      G<b>A</b>MING
    </h1>
  </section>
</template>

<script lang="ts" setup>
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/all';

gsap.registerPlugin(ScrollTrigger)

const totalVideosNumber = 4;

const isLoading = ref(true);
const isAnimating = ref(false);

const currentIndex = ref(1);
const hasClicked = ref(false);
const loadedVideos = ref(0);

const nextVideoRef = ref(null);
const currentVideoRef = ref(null);

const handleMiniVideoClick = () => {
  if (isAnimating.value) return; // Prevent clicks during animation

  hasClicked.value = true;
  currentIndex.value = (currentIndex.value % totalVideosNumber) + 1;
};

const getVideoSrc = (index: number) => {
  const safeIndex = (index - 1 + totalVideosNumber) % totalVideosNumber + 1;
  return `/videos/hero-${safeIndex}.mp4`;
};

const handleVideoLoad = () => {
  loadedVideos.value += 1;
}

watch(currentIndex, async () => {
  if (hasClicked.value && nextVideoRef.value && currentVideoRef.value && !isAnimating.value) {
    isAnimating.value = true;  // Lock to prevent new clicks

    // Reset next-video styles
    gsap.set(nextVideoRef.value, {
      clearProps: 'all',
      visibility: 'hidden',
      scale: 0.5,
      width: '16rem',
      height: '16rem',
    });

    // Show and animate the next video
    gsap.set(nextVideoRef.value, { visibility: 'visible' });

    gsap.to(nextVideoRef.value, {
      transformOrigin: 'center center',
      scale: 1,
      width: '100%',
      height: '100%',
      duration: 1,
      ease: 'power1.inOut',
      onStart: () => {
        nextVideoRef.value?.play();
      }
    });

    // Animate current video out
    await gsap.fromTo(currentVideoRef.value,
      {
        transformOrigin: 'center center',
        scale: 0,
        opacity: 0,
      },
      {
        scale: 1.5,
        opacity: 1,
        duration: 1,
        ease: 'power1.inOut',
      }
    );

    // After animation is done, unlock for next click
    isAnimating.value = false;
  }
});

onMounted(() => {
  gsap.set("#video-frame", {
    clipPath: "polygon(15% 0%, 70% 0%, 90% 90%, 0% 85%)",
    borderRadius: "0% 0% 30% 0%",
  });
  
   gsap.from("#video-frame", {
    clipPath: "polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)",
    borderRadius: "0% 0% 0% 0%",
    ease: "power1.inOut",
    scrollTrigger: {
      trigger: "#video-frame",
      start: "center center",
      end: "bottom top",
      scrub: true,
    },
  });
});

</script>

<style scoped lang="css">

</style>