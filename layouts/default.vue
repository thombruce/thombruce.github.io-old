<template lang='pug'>
#appContainer
  main
    Nuxt
</template>

<script>
import { themeChange } from 'theme-change'

export default {
  mounted () {
    themeChange(false)
  }
}
</script>
