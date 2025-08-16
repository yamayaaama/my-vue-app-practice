<template>
  <div class="dashboard">
    <h2>Dashboard</h2>
    <div v-if="user" class="user-info">
      <img src="user.photoURL" alt="プロフィール画像" class="profile-img">
      <p>ようこそ、{{ user.displayName || 'ユーザー' }}さん！</p>
      <p>メールアドレス: {{ user.email }}</p>
      <button @click="logout" class="logout-btn">ログアウト</button>
    </div>
    <div v-else>
      <p>読み込み中</p>
    </div>
  </div>
</template>

<script>
import { signOut } from 'firebase/auth';
import { auth } from '@/firebase';

export default {
  name: 'UserDashboard',
  props: ['user'],
  methods: {
    async logout() {
      try {
        await signOut(auth)
        console.log('ログアウトしました')
      } catch (error) {
        console.error('ログアウトエラー:', error)
      }
    }
  }
}
</script>

<style>
.dashboard {
  text-align: center;
  padding: 50px;
}

.profile-img {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin: 20px;
}

.logout-btn {
  background: #dc3545;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}

</style>