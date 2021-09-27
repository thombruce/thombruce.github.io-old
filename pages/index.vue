<template lang='pug'>
article.h-full
  .table-container
    table
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

<style lang='postcss' scoped>
.table-container {
  @apply w-full h-full overflow-auto;

  & table {
    @apply table w-full h-full;

    & th {
      &:first-child {
        @apply relative sm:sticky;
      }
    }

    & thead {
      & th {
        @apply sticky;
        top: 0;
        z-index: 20;
        &:first-child {
          @apply sticky left-auto sm:left-0;
          z-index: 30;
        }
      }
    }

    & thead, & tfoot {
      & th, & td {
        &:first-child {
          @apply rounded-l-none;
        }

        &:last-child {
          @apply rounded-r-none;
        }
      }
    }

    & td {
      @apply whitespace-normal;
    }
  }
}
</style>