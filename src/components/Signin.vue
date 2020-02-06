<template>
  <div class="signin">
    <h2>Sign in</h2>
    <input type="text" placeholder="Username" v-model="username">
    <input type="password" placeholder="Password" v-model="password">
    <button v-if="isAuth" @click="signOut" >Logout</button>
    <button v-else @click="signIn" >Signin</button>
    <button @click="signInByGoogle" >Google Signup</button>
  </div>
</template>

<script>
import firebase from 'firebase'

export default {
  name: 'signIn',
  data () {
    return {
      isAuth: false
    }
  },
  mounted: function () {
    firebase.auth().onAuthStateChanged((user) => { this.isAuth = !!user })
    alert('Success!')
    this.$router.push('/')
  },
  methods: {
    signIn: function () {
      firebase.auth().signInWithEmailAndPassword(this.username, this.password).then(
        user => {
          alert('Success!')
          this.$router.push('/')
        },
        err => {
          alert(err.message)
        }
      )
    },
    signInByGoogle: function () {
      const provider = new firebase.auth.GoogleAuthProvider()
      firebase.auth().signInWithRedirect(provider)
    },
    signOut: function () {
      firebase.auth().signOut()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.signin {
  margin-top: 20px;

  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center
}
input {
  margin: 10px 0;
  padding: 10px;
}
</style>
