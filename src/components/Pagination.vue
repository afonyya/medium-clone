<template lang="html">
  <ul class="pagination">
    <li
      v-for="page in pages"
      :key="page"
      :class="{ active: currentPage === page }"
      class="page-item"
    >
      <router-link
        :to="{
          path: url,
          query: { page }
        }"
        class="page-link"
      >
        {{ page }}
      </router-link>
    </li>
  </ul>
</template>

<script>
import { range } from '@/helpers/utils'

export default {
  name: 'Pagination',
  props: {
    total: {
      type: Number,
      required: true
    },
    limit: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    },
    url: {
      tupe: String,
      required: true
    }
  },
  computed: {
    pages () {
      const pagesCount = Math.ceil(this.total / this.limit)
      return range(1, pagesCount)
    }
  }
}
</script>
