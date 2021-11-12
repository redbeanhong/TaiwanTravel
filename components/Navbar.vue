<template lang="pug">
  nav(class="navbar navbar__border navbar-expand-lg fixed-top navbar-dark p-4")
    .container
      NuxtLink(class="navbar-brand" to="/") TAIWAN TRAVEL
      button(class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation")
        span(class="navbar-toggler-icon")
      .collapse.navbar-collapse.justify-content-end(id="navbarNavAltMarkup")
        .navbar-nav
          NuxtLink(class="nav-link" to="/") 首頁
          NuxtLink(class="nav-link" to="Tourism") 景點查詢
          NuxtLink(class="nav-link" to="Food") 美食推薦
          NuxtLink(class="nav-link" to="Hotel") 旅宿資訊
          NuxtLink(class="nav-link disabled" to="Show") 節慶活動
</template>
