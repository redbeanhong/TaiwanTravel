<template lang="pug">
  .banner(:class="bannerClass")
    .banner__mask
      img.banner__logo.my-4(src="@/assets/img/logo/logo--white.svg", alt="logo" v-if="logoWhite")
      img.banner__logo.my-4(src="@/assets/img/logo/logo--black.svg", alt="logo" v-else)
      .row.g-3.bg-light.rounded(v-if="this.$route.name==='index'")
        .col-lg-auto.input--mid
          select(class="form-select" aria-label="Default select example")
            option(selected) 北部地區
            option(value="1") One
            option(value="2") Two
            option(value="3") Three
        .col-lg-auto.input--mid
          select(class="form-select" aria-label="Default select example")
            option(selected) 台北市
            option(value="1") One
            option(value="2") Two
            option(value="3") Three
        .col-lg-auto.banner__search
          button(type="submit" class="btn btn-warning mb-3 text-light") SEARCH
</template>
<script>
export default {
  data() {
    return {
      bannerDate: [
        {
          name: 'index',
          bannerClass: 'banner--index',
          logoWhite: true
        },
        {
          name: 'Food',
          bannerClass: 'banner--food',
          logoWhite: false
        },
        {
          name: 'Hotel',
          bannerClass: 'banner--hotel',
          logoWhite: false
        },

        {
          name: 'Tourism',
          bannerClass: 'banner--tourism',
          logoWhite: true
        }
      ]
    }
  },
  computed: {
    routerName() {
      const name = this.$route.name
      return !name.includes('-') ? name : name.substr(0, name.indexOf('-'))
    },
    bannerClass() {
      const bannerClass = {}
      this.bannerDate.forEach((e) => {
        bannerClass[e.bannerClass] = e.name === this.$route.name
      })
      return bannerClass
    },
    logoWhite() {
      return this.bannerDate.find((e) => e.name === this.$route.name).logoWhite
    }
  }
}
</script>
