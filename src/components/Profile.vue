<template>
  <h1>Welcome, {{user.username}}</h1>
</template>

<script>
import { Auth } from "aws-amplify"

// Returns a user object with metadata 
export default {
  name: "Profile",
  data() {
    return {
      user: {}
    }
  },
  beforeCreate() {
      // or errors out if user not signed in.
    Auth.currentAuthenticatedUser()
      .then(user => {
        this.user = user
      })
      .catch(() => console.log("Not signed in..."))
  }
}
</script>
