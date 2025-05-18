<template lang="html">
  <section class="bg-black pb-52">
    <div class="container mx-auto px-4 md:px-10">
      <div class="px-5 py-32">
        <p class="font-circular-web text-lg text-blue-50">
          Into the  Metagame Layer
        </p>
        <p class="max-w-md font-circular-web text-lg text-blue-50 opacity-50">
          Immerse your self in a rich and ever-expanding universe where a vibrant array of products converge into an interconnected overlay experience on your world.
        </p>
      </div>

      <div class="px-2">
        <div class="mb-8 h-96 w-full md:h-[60vh]">
          <BentoCard 
            src="videos/feature-1.mp4"
            title="radia<b>n</b>t"
            description="A cross-platform metagame app, turning your activities across Web2 and Web3 games into a rewarding adventure."
            isComingSoon
          />
        </div>
        
        <div class="grid h-[135vh] w-full grid-cols-2 grid-rows-3 max-md:grid-cols-1 gap-8">
          <div class="bento-tilt_1 row-span-2 max-md:col-span-2 max-md:row-span-1">
            <BentoCard 
              src="videos/feature-2.mp4"
              title="zig<b>m</b>a"
              description="An anime and gaming-inspired NFT collection - the IP primed for expansion."
              isComingSoon
            />
          </div>

          <div class="bento-tilt_1 cols-span-1 row-span-1 max-md:col-span-2 ms-32 md:ms-0">
            <BentoCard 
              src="videos/feature-3.mp4"
              title="n<b>e</b>xus"
              description="A gamified social hub, adding a new dimension of play to social interaction for Web3 communities."
              isComingSoon
              isLaunchReady
            />
          </div>

          <div class="bento-tilt_1 col-span-1 row-span-1 max-md:col-span-2 me-14 md:me-0">
            <BentoCard 
              src="videos/feature-4.mp4"
              title="az<b>u</b>l"
              description="A cross-world AI Agent - elevating your gameplay to be more fun and productive."
              isComingSoon
            />
          </div>

          <div class="bento-tilt_2 col-span-2 md:col-span-1 max-md:order-1">
            <div class="flex size-full flex-col justify-between bg-violet-300 p-5">
              <h1 class="bento-title special-font max-w-64 text-black">
                M<b>o</b>re co<b>m</b>ing so<b>o</b>n!
              </h1>
              <NuxtImg 
                src="/img/Zentry Logo/zentry-symbol-black.png"
                width="92"
                height="92"
                class="self-end"
              />
            </div>
          </div>

          <div class="bento-tilt_2 col-span-2 md:col-span-1">
            <video 
              src="/videos/feature-5.mp4"
              loop
              muted
              autoplay
              class="size-full object-cover object-center"
            />
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<script lang="ts" setup>

</script>

<style>

</style>