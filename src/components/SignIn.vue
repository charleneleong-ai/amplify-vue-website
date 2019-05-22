<template>
  <div>
    <h2>Sign In</h2>
    <div class='formcontainer'>
      <input v-model='form.username' class='input' />
      <input type='password' v-model='form.password' class='input' />
      <button v-on:click='signIn' class='button'>Sign In</button>
    </div>
  </div>
</template>

<script>
import { Auth } from 'aws-amplify'
import { AmplifyEventBus } from 'aws-amplify-vue'
export default {
  name: 'home',
  data() {
    return {
      form: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
      // Sign in the user calling Auth.signIn 
    async signIn() {
      const { username, password } = this.form
      await Auth.signIn(username, password)
      // If user signs in, emits authState of signedIn to redirect them to profile
      // authState listener in App.vue
      AmplifyEventBus.$emit('authState', 'signedIn')
      this.$router.push('/profile')
    }
  }
}
</script>