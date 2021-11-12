<template lang="pug">
  div
    Navbar
    Banner
    nuxt
    Footerbar
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Banner from '@/components/Banner.vue'
import Footerbar from '@/components/Footerbar.vue'
export default {
  components: {
    Navbar,
    Banner,
    Footerbar
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/all.scss';
</style>
