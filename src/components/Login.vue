<template>
  <div class="login">
    <h2>ログイン</h2>
    <button @click="signInWithGoogle" class="google-btn">
      Googleでログイン
    </button>
  </div>
</template>

<script>
import { GoogleAuthProvider, signInWithPopup } from 'firebase/auth';
import { auth } from '@/firebase';

export default {
  name: 'UserLogin',
  methods: {
    async signInWithGoogle() {
      try {
        const provider = new GoogleAuthProvider()
        await signInWithPopup(auth, provider)
        console.log('ログイン成功')
      } catch (error) {
        console.error('ログインエラー', error)
      }
    }
  }
}
</script>

<style>
.login {
  text-align: center;
  padding: 50px;
}

.google-btn {
  background-color: #4285f4;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 20px;
}
</style>