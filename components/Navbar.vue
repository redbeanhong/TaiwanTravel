<template lang="pug">
  nav(class="navbar navbar-expand-lg navbar-dark bg-info")
    .container
      a(class="navbar-brand" href="#") TAIWAN TRAVEL
      button(class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation")
        span(class="navbar-toggler-icon")
      .collapse.navbar-collapse.justify-content-end(id="navbarNavAltMarkup")
        .navbar-nav
          NuxtLink(class="nav-link disabled" to="Travel") 旅遊情報
          NuxtLink(class="nav-link" to="/") 景點查詢
          NuxtLink(class="nav-link" to="Food") 美食推薦
          NuxtLink(class="nav-link" to="Hotel") 旅宿資訊
          NuxtLink(class="nav-link disabled" to="Show") 節慶活動
</template>
