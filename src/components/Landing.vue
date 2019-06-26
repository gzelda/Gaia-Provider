<template>
  <div class="hello">
    <div>
      <h1>Gaia-Provider IOT System</h1>
      <h3>Can't be evil</h3>
      <button class="btn btn-default bg-white" >Sign In With MetaMask</button>
      <br><br>

      <button class="btn btn-default bg-white" @click.prevent="signIn">Sign In With Blockstack</button>
    </div>
  </div>
</template>

<script>
import { userSession } from '../userSession'

export default {
  name: 'landing',
  methods: {
    signIn () {
      userSession.redirectToSignIn()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
