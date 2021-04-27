<template lang="html">
  <div class="home-page">
    BANNER
    <div class="container page">
      <div class="row">
        <div class="col-md-9">
          <Feed :api-url="apiUrl" />
        </div>
        <div class="col-md-3">
          <PopularTags />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Feed from '@/components/Feed.vue'
import PopularTags from '@/components/PopularTags.vue'

export default {
  name: 'GlobalFeed',
  components: {
    Feed,
    PopularTags
  },
  data () {
    return {
      apiUrl: '/articles'
    }
  }
}
</script>
