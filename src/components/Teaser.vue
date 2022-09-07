<template>
  <div class="bg-contain bg-bottom lg:bg-right bg-no-repeat w-full h-screen p-0 lg:p-16 bg-off-white lg:bg-desktop relative">
    <!-- <section ref="header" class="relative lg:hidden w-full flex flex-col items-center justify-center pt-5 xs:pt-8 pb-2">
      <img alt="Gallycat logo" src="../assets/gallycat_logo_3x.png" class="w-16 xs:w-20 object-fit" @load="onLogoLoad">
      <h1 class="text-dark font-bold text-4xl xs:text-4.5xl whitespace-nowrap mt-4 xs:mt-8 leading-tight">Coming soon</h1>
    </section>

    <section class="lg:hidden bg-mobile bg-cover bg-no-repeat bg-center relative w-full" :style="{height: mobileBodyH + 'px'}">
      <div class="absolute inset-x-0 bottom-8 flex justify-center">
        <div class="p-3 animate-bounce rounded-full bg-white bg-opacity-75">
          <img alt="arrow down" src="../assets/arrow_down.svg" class="w-8 opacity-50">
        </div>
      </div>
    </section> -->
    <section class="lg:hidden w-full bg-se xs:bg-mobile bg-cover bg-bottom relative" :style="{ height: innerH + 'px' }">
      <div class="relative w-full flex flex-col items-center justify-center pt-5 xs:pt-8 pb-6 bg-se-linear xs:bg-none">
        <img alt="Gallycat logo" src="../assets/gallycat_logo_3x.png" class="w-12 xs:w-20 object-fit">
        <h1 class="text-dark font-bold text-4xl xs:text-4.5xl whitespace-nowrap mt-4 xs:mt-8 leading-tight">Coming soon</h1>
      </div>
      <div class="absolute inset-x-0 bottom-8 flex justify-center">
        <div class="p-3 animate-bounce rounded-full bg-white bg-opacity-75">
          <img alt="arrow down" src="../assets/arrow_down.svg" class="w-8 opacity-50">
        </div>
      </div>
    </section>


    <section class="w-full lg:w-1/2 p-8 lg:p-0" id="desktop-content">
      <img alt="Gallycat logo" src="../assets/gallycat_logo_3x.png" class="w-32 object-fit hidden lg:block">
      <h1 class="text-dark font-bold text-90px mt-10 leading-tight hidden lg:block">Coming soon</h1>
      <h2 class="text-sec font-bold text-4xl mt-6 leading-none">The future hub of culinary curators</h2>
      <p class="text-dark text-xl lg:text-3xl mt-2 font-medium lg:font-normal">Explore gastronomy trails marked by your favourite, most trusted foodies.</p>
    </section>

    <footer class="flex justify-center lg:fixed lg:inset-x-0 lg:bottom-0 bg-black bg-opacity-70 lg:py-12 p-8">
      <div class="mx-auto grid grid-cols-1 gap-8 lg:gap-4">
        <div class="text-white text-lg text-center leading-snug font-medium">Don't miss out on exclusive early access. Join the waiting list today!</div>
        <section class="flex lg:flex-row flex-col items-center space-y-3 lg:space-y-0 lg:space-x-4 justify-center">
          <input type="text" class="bg-white rounded-xl py-2 px-3 lg:grow w-full lg:w-auto" placeholder="email">
          <button class="bg-pri text-white py-2 px-5 w-full lg:w-auto rounded-xl">Sign me up!</button>
        </section>
      </div>

    </footer>
  </div>
</template>

<script>
  export default {
    name: 'TeaserPage',
    data() {
      return {
        mobileHeaderH: null,
        mobileBodyH: null,
        innerH: window.innerHeight
      }
    },
    methods: {
      onLogoLoad() {
        const mobileHeader = this.$refs.header
        this.mobileHeaderH = mobileHeader.offsetHeight
        this.mobileBodyH = window.innerHeight - mobileHeader.offsetHeight
        console.log(222, 'header', this.mobileHeaderH, 'body', this.mobileBodyH)
      }
    },
    mounted() {
      console.log('window dimension:', window.innerHeight, window.innerWidth)
      const mobileHeader = this.$refs.header
      console.log(mobileHeader.offsetHeight)

      this.mobileHeaderH = mobileHeader.offsetHeight
      this.mobileBodyH = window.innerHeight - mobileHeader.offsetHeight
      console.log(111, 'header', this.mobileHeaderH, 'body', this.mobileBodyH)
    }
  }
</script>

<style scoped>

</style>
