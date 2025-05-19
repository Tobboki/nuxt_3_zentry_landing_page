<template>
  <section id="contact" class="my-20 min-h-96 w-screen px-10">
    <div class="relative rounded-lg bg-black py-24 text-blue-50 sm:overflow-hidden">
      <div class="pointer-events-none">
        <figure class="absolute -left-10 top-0 h-full w-72 overflow-hidden sm:block lg:left-20 lg:w-96">
          <ImageClipBox
            src="/img/contact-1.webp"
            clip-class="contact-clip-path-1 max-sm:hidden"
            alt="Contact illustration"
          />
          <ImageClipBox
            src="/img/contact-2.webp"
            clip-class="contact-clip-path-2 lg:translate-y-5 translate-y-20 max-sm:translate-y-60 z-50"
            alt="Additional contact illustration"
          />
        </figure>

        <figure class="absolute -top-40 left-90 w-60 sm:top-1/2 md:left-auto md:right-10  max-sm:left-1/4 max-sm:-top-1/4 lg:top-40 lg:w-80">
          <ImageClipBox
            src="/img/swordman-partial.webp"
            clip-class="absolute md:scale-125"
            alt="Partial swordman character"
          />
          <ImageClipBox
            src="/img/swordman.webp"
            clip-class="sword-man-clip-path md:scale-125"
            alt="Swordman character artwork"
          />
        </figure>
      </div>

      <!-- Main content -->
      <div class="flex flex-col items-center text-center">
        <header class="mb-10">
          <p class="font-general text-[10px] uppercase">Join Zentry</p>
          <AnimatedTitle
            title="let&#39;s b<b>u</b>ild the <br /> new era of <br /> g<b>a</b>ming t<b>o</b>gether."
            container-class="special-font !md:text-[6.2rem] w-full font-zentry !text-5xl !font-black !leading-[.9]"
            text-class="text-blue-50"
          />
        </header>

        <footer class="mt-10">
          <Button 
            title="contact us"
          />
        </footer>
      </div>
    </div>
  </section>
</template>

<script setup>

</script>

<style>

</style>