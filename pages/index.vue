<template lang='pug'>
article.m-4
  .overflow-x-auto
    table.table.w-full
      thead
        tr
          th Name
          th Description
          th Language
          th Git
      tbody
        tr(v-for='(repo, i) in repos')
          th
            a(v-if='repo.homepage' :href='repo.homepage') {{ repo.name }}
            span(v-else) {{ repo.name }}
          td {{ repo.description }}
          td {{ repo.language }}
          td
            a(:href='repo.html_url') {{ repo.full_name }}
</template>

<script>
export default {
  async asyncData ({ $axios }) {
    const repos = await $axios.$get('https://api.github.com/users/thombruce/repos?per_page=100&type=public&sort=updated')
    
    return { repos }
  },

  head () {
    return {
      titleTemplate: null
    }
  }
}
</script>

<style lang='postcss'>
.table {
  & th {
    &:first-child {
      @apply relative sm:sticky;
    }
  }

  & td {
    @apply whitespace-normal;
  }
}
</style>