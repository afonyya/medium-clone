<template lang="html">
  <nav class="navbar navbar-light">
    <div class="container">
      <router-link
        :to="{ name: 'globalFeed' }"
        class="navbar-brand"
      >
        MediumClone
      </router-link>
      <ul class="nav navbar-nav pull-xs-right">
        <li class="nav-item">
          <router-link
            :to="{ name: 'globalFeed' }"
            class="nav-link"
            exact
            active-class="active"
          >
            Home
          </router-link>
        </li>
        <template v-if="isLoggedIn">
          <li class="nav-item">
            <router-link
              :to="{ name: 'createArticle' }"
              class="nav-link"
              active-class="active"
            >
              <i class="ion-compose"></i> &nbsp; New Article
            </router-link>
          </li>

          <li class="nav-item">
            <router-link
              :to="{ name: 'settings' }"
              class="nav-link"
              active-class="active"
            >
              <i class="ion-gear-a"></i> &nbsp; Settings
            </router-link>
          </li>

          <li class="nav-item">
            <router-link
              :to="{
                name: 'userProfile',
                params: { slug: currentUser.username }
              }"
              class="nav-link"
              active-class="active"
            >
              <img
                :src="currentUser.image"
                class="user-pic"
              />
              &nbsp;
              {{ currentUser.username }}
            </router-link>
          </li>
        </template>

        <template v-if="isAnonymous">
          <li class="nav-item">
            <router-link
              :to="{ name: 'login' }"
              class="nav-link"
              active-class="active"
            >
              Sign in
            </router-link>
          </li>

          <li class="nav-item">
            <router-link
              :to="{ name: 'register' }"
              class="nav-link"
              active-class="active"
            >
              Sign up
            </router-link>
          </li>
        </template>
      </ul>
    </div>
  </nav>
</template>

<script>
import { getterTypes } from '@/store/modules/auth'
import { mapGetters } from 'vuex'

export default {
  name: 'TopBar',
  computed: {
    ...mapGetters({
      currentUser: getterTypes.currentUser,
      isLoggedIn: getterTypes.isLoggedIn,
      isAnonymous: getterTypes.isAnonymous
    })
  }
}
</script>
