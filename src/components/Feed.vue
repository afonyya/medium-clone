<template lang="html">
  <div>
    <Loading v-if="isLoading" />
    <ErrorMessage v-if="error" />
    
    <div v-if="feed">
      <div
        v-for="(article, index) in feed.articles"
        :key="index"
        class="article-preview"
      >
        <div class="article-meta">
          <router-link
            :to="{
              name: 'userProfile',
              params: { slug: article.author.username }
            }"
          >
            <img :src="article.author.image" />
          </router-link>
          <div class="info">
            <router-link
              :to="{
                name: 'userProfile',
                params: { slug: article.author.username }
              }"
              class="author"
            >
              {{ article.author.username }}
            </router-link>
            <span class="date">{{ article.createdAt }}</span>
          </div>
          <div class="pull-xs-right">
            ADD TO FAVORITES
          </div>
        </div>
        <router-link
          :to="{
            name: 'article',
            params: { slug: article.slug }
          }"
          class="preview-link"
        >
          <h3>{{ article.title }}</h3>
          <p>{{ article.description }}</p>
          <span>Reed more...</span>
          TAG LIST
        </router-link>
      </div>
      <Pagination
        :total="feed.articlesCount"
        :limit="limit"
        :current-page="currentPage"
        :url="baseUrl"
      />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { actionTypes } from '@/store/modules/feed'
import Pagination from '@/components/Pagination.vue'
import { limit } from '@/helpers/vars'
import { stringify, parseUrl } from 'query-string'
import Loading from '@/components/Loading.vue'
import ErrorMessage from '@/components/ErrorMessage.vue'

export default {
  name: 'Feed',
  components: {
    Pagination,
    Loading,
    ErrorMessage
  },
  props: {
    apiUrl: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      limit
    }
  },
  computed: {
    ...mapState({
      isLoading: state => state.feed.isLoading,
      feed: state => state.feed.data,
      error: state => state.feed.error
    }),
    currentPage () {
      return +this.$route.query.page || 1
    },
    baseUrl () {
      return this.$route.path
    },
    offset () {
      return this.currentPage * limit - limit
    }
  },
  watch: {
    currentPage () {
      this.fetchFeed()
    }
  },
  methods: {
    fetchFeed () {
      const parsedUrl = parseUrl(this.apiUrl)
      const stringifiedParams = stringify({
        limit,
        offset: this.offset,
        ...parsedUrl.query
      })
      const apiUrlWithParams = `${parsedUrl.url}?${stringifiedParams}`
      this.$store.dispatch(actionTypes.getFeed, { apiUrl: apiUrlWithParams })
    }
  },
  mounted () {
    this.fetchFeed()
  }
}
</script>
