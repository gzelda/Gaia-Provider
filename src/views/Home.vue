<template>
  <div id="app">
    <landing v-if="! userSession.isUserSignedIn()"></landing>
    <userinfo v-if="user" :user="user"></userinfo>

    <small class="creds">
      todo
      Source code on <a href="https://github.com/blockstack/blockstack-todos" target="_blank">Github</a>
    </small>
  </div>
</template>

<script>
import Landing from '@/components/Landing.vue'
import Userinfo from '@/components/Userinfo.vue'
import Rawdata from '@/components/Rawdata.vue'
import { Person } from 'blockstack'
import { userSession } from '../userSession'

export default {
  name: 'Home',
  components: { Landing, Userinfo },
  created () {
    this.userSession = userSession
  },
  mounted () {
    if (userSession.isUserSignedIn()) {
      this.userData = userSession.loadUserData()
      this.user = new Person(this.userData.profile)
      this.user.username = this.userData.username
    } else if (userSession.isSignInPending()) {
      userSession.handlePendingSignIn()
        .then((userData) => {
          window.location = window.location.origin
        })
    }
  },
  data () {
    return {
      userSession: null,
      user: null
    }
  }
}
</script>
