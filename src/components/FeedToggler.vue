<template lang="html">
  <div class="feed-toggle">
    <ul class="nav nav-pills outline-active">
      <li
        v-if="isLoggedIn"
        class="nav-item"
      >
        <router-link
          :to="{ name: 'yourFeed' }"
          :class="{ active: routeName === 'yourFeed' }"
          class="nav-link"
        >
          Your Feed
        </router-link>
      </li>

      <li class="nav-item">
        <router-link
          :to="{ name: 'globalFeed' }"
          :class="{ active: routeName === 'globalFeed' }"
          class="nav-link"
        >
          Global Feed
        </router-link>
      </li>

      <li
        v-if="tagName"
        class="nav-item"
      >
        <router-link
          :to="{ name: 'tag' }"
          :class="{ active: routeName === 'tag' }"
          class="nav-link"
        >
          <i class="ion-pound" />
          {{ tagName }}
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { getterTypes } from '@/store/modules/auth'

export default {
  name: 'FeedToggler',
  props: {
    tagName: {
      type: String,
      required: false
    }
  },
  computed: {
    ...mapGetters({
      isLoggedIn: getterTypes.isLoggedIn
    }),
    routeName () {
      return this.$route.name
    }
  }
}
</script>
