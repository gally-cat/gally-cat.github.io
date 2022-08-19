<template>
  <TeaserPage />
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TeaserPage from './components/Teaser.vue'

export default {
  name: 'App',
  components: {
    TeaserPage
  }
}
</script>

<style>
@font-face {
  font-family: 'Work-Sans';
  src: url('https://res.cloudinary.com/dztwrgpbi/raw/upload/v1660876797/gallycat/fonts/work_sans/WorkSans-Regular.ttf');
  font-weight: 400;
  font-style: 'normal';
}

@font-face {
  font-family: 'Work-Sans';
  src: url('https://res.cloudinary.com/dztwrgpbi/raw/upload/v1660876795/gallycat/fonts/work_sans/WorkSans-Medium.ttf');
  font-weight: 500;
  font-style: 'normal';
}

@font-face {
  font-family: 'Work-Sans';
  src: url('https://res.cloudinary.com/dztwrgpbi/raw/upload/v1660876795/gallycat/fonts/work_sans/WorkSans-SemiBold.ttf');
  font-weight: 600;
  font-style: 'normal';
}

@font-face {
  font-family: 'Work-Sans';
  src: url('https://res.cloudinary.com/dztwrgpbi/raw/upload/v1660876793/gallycat/fonts/work_sans/WorkSans-Bold.ttf');
  font-weight: 700;
  font-style: 'normal';
}

#app {
  font-family: 'Work-Sans', Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
