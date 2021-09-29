<template lang='pug'>
article.h-full
  .table-container
    table
      thead
        tr
          th Name
          th Description
          th Language
          th.text-center Git
          th.text-center Issues
      tbody
        tr(v-for='(repo, i) in repos')
          th
            a(v-if='repo.homepage' :href='repo.homepage') {{ repo.name }}
            span(v-else) {{ repo.name }}
          td {{ repo.description }}
          td {{ repo.language }}
          td.text-center
            a.text-lg(:href='repo.html_url')
              fa(:icon='faCodeBranch')
          td.text-center
            a.text-lg(:href="repo.html_url + '/issues'")
              .indicator
                .indicator-item.badge.badge-error {{ repo.open_issues_count }}
                fa(:icon='faBug')
</template>

<script>
import { faCodeBranch, faBug } from '@fortawesome/free-solid-svg-icons'

export default {
  async asyncData ({ $axios }) {
    const repos = await $axios.$get('https://api.github.com/users/thombruce/repos?per_page=100&type=public&sort=updated')
    
    return { repos }
  },

  async created () {
    this.repos = await this.$axios.$get('https://api.github.com/users/thombruce/repos?per_page=100&type=public&sort=updated')
  },

  computed: {
    faCodeBranch () {
       return faCodeBranch
    },
    faBug () {
      return faBug
    }
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