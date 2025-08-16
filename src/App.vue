<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <UserLogin v-if="!user" />
  <UserDashboard v-else :user="user" />
</template>

<script>
import { onAuthStateChanged } from 'firebase/auth';
import { auth } from '@/firebase';

import UserLogin from './components/Login.vue'
import UserDashboard from '@/components/Dashbord.vue'

export default {
  name: 'App',
  components: {
    UserLogin,
    UserDashboard
  },
  data() { //コンポーネントがマウントされたときに実行される
    console.log('Appコンポーネントがマウントされました')
    return {
      user: null
    }
  },
  mounted() {
    onAuthStateChanged(auth, (user) => {
      this.user = user
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
