<template lang="html">
  <div>
    CreateArticle
    <ArticleForm
      :initial-values="initialValues"
      :errors="validationErrors"
      :is-submitting="isSubmitting"
      @articleSubmit="onSubmit"
    />
  </div>
</template>

<script>
import ArticleForm from '@/components/ArticleForm.vue'

export default {
  name: 'CreateArticle',
  components: {
    ArticleForm
  },
  data () {
    return {
      initialValues: {
        title: '',
        description: '',
        body: '',
        tagList: []
      },
      validationErrors: null,
      isSubmitting: false
    }
  },
  methods: {
    onSubmit (data) {
      console.log('submit', data)
    }
  }
}
</script>
