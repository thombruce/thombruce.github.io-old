<template lang='pug'>
.h-screen.flex.flex-col
  header.flex-none
    .navbar
      .navbar-start
        h1.text-lg.font-bold
          NuxtLink(to='/') Thom Bruce
      .navbar-center
        span Repositories
      .navbar-end
        span thombruce.github.io
  main.flex-1.overflow-auto
    Nuxt
  footer.flex-none.footer.footer-center
    div
      p © Thom Bruce 2021
</template>

<script>
import { themeChange } from 'theme-change'

export default {
  mounted () {
    themeChange(false)
  }
}
</script>
