<template>
  <div id="app">
    <login-page v-if="!auth" @resp-ok="respOk" @login-user="loginUser"/>
    <user-page v-if="auth" @to-auth-page="toAuthPage" />
  </div>
</template>

<script>
import LoginPage from './components/pages/LoginPage';
import UserPage from './components/pages/UserPage';

export default {
  data() {
    return {
      auth: false
    }
  }, 

  name: 'App',
  components: {
    LoginPage,
    UserPage
  },

  methods: {
    respOk( data ) {
      console.log( data );
    },

    toAuthPage() {
      this.auth = false
    },

    loginUser() {
      this.auth = true
    }
  }
}
</script>

<style lang="scss">

body {
  margin: 0;
}

  ::-webkit-scrollbar {
      display: none;
  }


</style>
