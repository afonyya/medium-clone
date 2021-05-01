<template lang="html">
  <div
    v-if="currentUser"
    class="settings-page"
  >
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h2 class="text-xs-center">Settings</h2>
          <ValidationErrors
            v-if="validationErrors"
            :validation-errors="validationErrors"
          />
          <form @submit.prevent="onSubmit">
            <fieldset>
              <fieldset class="form-group">
                <input
                  v-model="form.image"
                  type="text"
                  class="form-control form-control-lg"
                  placeholder="URL of profile picture"
                />
              </fieldset>

              <fieldset class="form-group">
                <input
                  v-model="form.username"
                  type="text"
                  class="form-control form-control-lg"
                  placeholder="User Name"
                />
              </fieldset>

              <fieldset class="form-group">
                <textarea
                  v-model="form.bio"
                  class="form-control form-control-lg"
                  placeholder="Short bio about you"
                ></textarea>
              </fieldset>

              <fieldset class="form-group">
                <input
                  v-model="form.email"
                  type="text"
                  class="form-control form-control-lg"
                  placeholder="Email"
                />
              </fieldset>

              <fieldset class="form-group">
                <input
                  v-model="form.password"
                  type="password"
                  class="form-control form-control-lg"
                  placeholder="Password"
                />
              </fieldset>
              <button
                :disabled="isSubmitting"
                type="submit"
                class="btn btn-lg btn-primary pull-xs-right"
              >
                Update Settings
              </button>
            </fieldset>
          </form>
          <hr />
          <button
            @click="logout"
            type="text"
            class="btn btn-outline-danger"
          >
            Or click here to logout
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'
import {
  getterTypes as authGetterTypes,
  actionTypes as authActionTypes
} from '@/store/modules/auth'
import ValidationErrors from '@/components/ValidationErrors.vue'

export default {
  name: 'Settings',
  components: {
    ValidationErrors
  },
  computed: {
    ...mapState({
      isSubmitting: state => state.settings.isSubmitting,
      validationErrors: state => state.settings.validationErrors
    }),
    ...mapGetters({
      currentUser: authGetterTypes.currentUser
    }),
    form () {
      return {
        username: this.currentUser.username,
        bio: this.currentUser.bio,
        image: this.currentUser.image,
        email: this.currentUser.email,
        password: ''
      }
    }
  },
  methods: {
    onSubmit () {
      this.$store.dispatch(authActionTypes.updateCurrentUser, { currentUserInput: this.form })
    },
    logout () {
      this.$store.dispatch(authActionTypes.logout)
        .then(() => this.$router.push({ name: 'globalFeed' }))
    }
  }
}
</script>
