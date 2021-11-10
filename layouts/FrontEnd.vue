<template lang="pug">
  div
    Navbar
    nuxt
    Footerbar
</template>

<script>
import Navbar from '@/components/Navbar.vue'
import Footerbar from '@/components/Footerbar.vue'
export default {
  components: {
    Navbar,
    Footerbar
  }
}
</script>

<style lang="scss">
@import '@/assets/scss/all.scss';
</style>
