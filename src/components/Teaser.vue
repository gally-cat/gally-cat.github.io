<template>
  <!-- <div class="bg-contain bg-bottom lg:bg-right bg-no-repeat w-full h-screen p-0 lg:p-16 bg-white lg:bg-off-white lg:bg-desktop relative"> -->
  <div class="bg-contain bg-bottom lg:bg-right bg-no-repeat w-full lg:h-screen p-0 lg:p-16 bg-off-white lg:bg-desktop relative">

    <section class="lg:hidden w-full bg-se sm:bg-mobile md:bg-ipad bg-cover bg-no-repeat bg-center relative" :style="{ height: innerH + 'px' }">
      <div class="relative w-full flex flex-col items-center justify-center pt-5 sm:pt-8 pb-6 bg-mobile-header-gradient">
        <img alt="Gallycat logo" src="../assets/gallycat_logo_3x.png" class="w-12 sm:w-20 md:w-24 object-fit">
        <h1 class="text-dark font-bold text-4xl sm:text-4.5xl md:text-6xl whitespace-nowrap mt-4 sm:mt-8 md:mt-16 leading-tight">Coming Soon</h1>
      </div>
      <div class="absolute inset-x-0 bottom-8 flex justify-center" ref="arrow" @click="scrollToArrow">
        <div class="p-3 animate-bounce rounded-full bg-white bg-opacity-75">
          <img alt="arrow down" src="../assets/arrow_down.svg" class="w-8 opacity-50">
        </div>
      </div>
    </section>


    <section class="w-full lg:w-1/2 p-8 lg:p-0 mb-4 lg:mb-0">
      <img alt="Gallycat logo" src="../assets/gallycat_logo_3x.png" class="w-28 xl:w-32 object-fit hidden lg:block">
      <h1 class="text-dark font-bold text-6xl xl:text-90px mt-10 leading-tight hidden lg:block">Coming Soon</h1>
      <h2 class="text-sec font-bold text-3xl sm:text-4xl leading-none"
        :class="h2ClassList">
        The future hub of culinary curators
      </h2>
      <p class="text-dark text-xl lg:text-3xl mt-2 font-medium">Explore gastronomy trails marked by your favourite, most trusted foodies.</p>
    </section>

    <footer class="flex justify-center lg:fixed lg:inset-x-0 lg:bottom-0 bg-black bg-opacity-70 lg:py-12 px-8 py-10">
      <div class="mx-auto grid grid-cols-1 gap-8 lg:gap-4">
        <div class="text-white text-lg text-center leading-snug font-medium">Don't miss out on exclusive early access. Join the waiting list today!</div>
        <section class="flex lg:flex-row flex-col items-center space-y-3 lg:space-y-0 lg:space-x-4 justify-center">
          <div class="bg-white rounded-xl lg:grow w-full lg:w-auto relative"
            :class="{ 'border-2 border-error': emailSubmitError }">
            <div v-show="emailSubmitError" class="absolute right-2 inset-y-0 flex items-center">
              <img src="../assets/error.svg" class="w-4 h-4">
            </div>

            <input v-model="email" type="text"
              class="h-full w-full py-2 px-3 rounded-xl"
              placeholder="email">
          </div>

          <button
            :disabled="isSubmitting || emailSubmitSuccess"
            @click="submitEmail"
            class="bg-pri text-white leading-tight py-2 px-5 w-full lg:w-44 rounded-xl flex items-center justify-center">
            <span v-if="emailSubmitSuccess">Signed up!</span>
            <span v-else-if="isSubmitting">Signing up..</span>
            <span v-else>Sign me up!</span>
            <!-- <img src="../assets/loading.svg" class="w-4 h-4 ml-3 animate-spin"> -->
            <img v-if="emailSubmitSuccess" src="../assets/success.svg" class="w-4 h-4 ml-3">
            <img v-else-if="isSubmitting" src="../assets/loading.svg" class="w-4 h-4 ml-3 animate-spin">
          </button>
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
        email: null,
        emailSubmitError: false,
        emailSubmitSuccess: false,
        isSubmitting: false,
        innerH: window.innerHeight,
        innerW: window.innerWidth,
        isTall: ((window.innerHeight/window.innerWidth) >= 0.54),
        device: null,
        h2ClassList: null
      }
    },
    methods: {
      onLogoLoad() {
        const mobileHeader = this.$refs.header
        this.mobileHeaderH = mobileHeader.offsetHeight
        this.mobileBodyH = window.innerHeight - mobileHeader.offsetHeight
        console.log(222, 'header', this.mobileHeaderH, 'body', this.mobileBodyH)
      },
      scrollToArrow() {
        const el = this.$refs.arrow;
        if (el) {
          el.scrollIntoView({behavior: 'smooth'})
        }
      },
      deviceIs() {
        const mobile = [
          /Android/i,
          /webOS/i,
          /iPhone/i,
          // /iPad/i,
          /iPod/i,
          /BlackBerry/i,
          /Windows Phone/i,
        ]

        const ipad = /iPad/i

        if (navigator.userAgent.match(ipad) || (screen.orientation.type.includes('portrait') && window.innerWidth >= 768)) {
          return 'ipad'
        } else if (mobile.some((item) => navigator.userAgent.match(item))) {
          return 'mobile'
        } else {
          return 'desktop'
        }
      },
      handleOrientationChange() {
        // only handling ipad
        // if (orientation.includes('portrait')) {
          this.innerH = window.innerHeight
          this.innerW = window.innerWidth
        // }
      },
      submitEmail() {
        console.log('email:', this.email)
        if (!this.email) {
          // fetch
          this.emailSubmitError = true
        } else if (this.email.match(/^(.+)@(.+)$/)) {
          this.emailSubmitError = false
          this.isSubmitting = true
          fetch(`http://localhost:3000/submit_email?email=${this.email}`, {
            method: 'POST',
            // mode: "cors" // "no-cors"
          }).then((response) => response.json()).then((data) => {
            console.log(data)
            this.isSubmitting = false
            this.emailSubmitSuccess = true
          })
        } else {
          this.emailSubmitError = true
        }
      }
    },
    mounted() {
      console.log('window dimension:', window.innerHeight, window.innerWidth)
      // console.log('window', window)
      // console.log('window', window.devicePixelRatio)
      // console.log('userAgent', navigator.userAgent)
      this.device = this.deviceIs()
      if (this.isTall && (['desktop', 'ipad'].includes(this.device))) {
        this.h2ClassList = 'mt-8'
      } else if (this.device == 'desktop') {
        this.h2ClassList = 'mt-3'
      }
      console.log(this.device)
      console.log('orientation?', screen.orientation.type)
      if (this.device == 'mobile') screen.orientation.lock('portrait')
      screen.orientation.addEventListener('change', (e) => {
        console.log('orientation changed', e.srcElement)
        // if (this.device == 'ipad') this.handleOrientationChange(e.srcElement)
        if (this.device == 'ipad') this.handleOrientationChange()
      })
    }
  }
</script>

<style scoped>

</style>
