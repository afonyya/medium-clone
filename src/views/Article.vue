<template lang="html">
  <div class="article-page">
    <div class="banner">
      <div
        v-if="article"
        class="container"
      >
        <h3>{{ article.title }}</h3>
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
            >
              {{ article.author.username }}
            </router-link>
            <span class="date">{{ article.createdAt }}</span>
          </div>
          <span>
            <router-link
              :to="{
                name: 'editArticle',
                params: { slug: article.slug }
              }"
              class="btn btn-outline-secondary btn-sm"
            >
              <i class="ion-edit" />
              Edit Article
            </router-link>
            <button class="btn btn-outline-danger btn-sm">
              <i class="ion-trash-a" />
              Delete Article
            </button>
          </span>
        </div>
      </div>
    </div>
    <div class="container page">
      <Loading v-if="isLoading" />
      <ErrorMessage
        v-if="error"
        :message="error"
      />
      <div
        v-if="article"
        class="row article-content"
      >
        <div class="col-xs-12">
          <div>
            <p>{{ article.body }}</p>
          </div>
          TAGLIST
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { actionTypes } from '@/store/modules/article'
import { mapState } from 'vuex'
import Loading from '@/components/Loading.vue'
import ErrorMessage from '@/components/ErrorMessage.vue'

export default {
  name: 'Article',
  components: {
    Loading,
    ErrorMessage
  },
  computed: {
    ...mapState({
      isLoading: state => state.article.isLoading,
      error: state => state.article.error,
      article: state => state.article.data
    })
  },
  mounted () {
    this.$store.dispatch(actionTypes.getArticle, { slug: this.$route.params.slug })
  }
}
</script>
