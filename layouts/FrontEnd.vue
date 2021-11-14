<template lang="pug">
  div
    Navbar
    Banner
    .container
      Breadcrumb
      nuxt
    Footerbar
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Banner from '@/components/Banner.vue'
import Breadcrumb from '@/components/Breadcrumb.vue'
import Footerbar from '@/components/Footerbar.vue'
export default {
  components: {
    Navbar,
    Banner,
    Breadcrumb,
    Footerbar
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/all.scss';
</style>
