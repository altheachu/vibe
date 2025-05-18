<script setup>
import { ref } from 'vue';

const userId = ref('');
const birthday = ref('');
const emit = defineEmits(['login']);

const handleLogin = () => {
  if (!userId.value || !birthday.value) {
    alert('請填寫所有欄位');
    return;
  }
  
  emit('login', { id: userId.value, birthday: birthday.value });
};
</script>

<template>
  <div class="login-card">
    <h1>心理諮商所診前問卷</h1>
    <div class="form-group">
      <label for="user-id">請輸入您的 ID</label>
      <input 
        id="user-id" 
        v-model="userId" 
        type="text" 
        placeholder="例如：A123或B123"
      >
    </div>
    
    <div class="form-group">
      <label for="birthday">請輸入您的生日</label>
      <input 
        id="birthday" 
        v-model="birthday" 
        type="date" 
      >
    </div>
    
    <button @click="handleLogin" class="login-btn">確認</button>
  </div>
</template>

<style scoped>
.login-card {
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  padding: 30px;
  max-width: 400px;
  width: 100%;
}

h1 {
  color: #6c5ce7;
  text-align: center;
  margin-bottom: 25px;
  font-size: 1.8rem;
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: 500;
  color: #2d3436;
}

input {
  width: 100%;
  padding: 12px;
  border: 2px solid #dfe6e9;
  border-radius: 8px;
  font-size: 16px;
  transition: border-color 0.3s;
}

input:focus {
  border-color: #6c5ce7;
  outline: none;
}

.login-btn {
  background-color: #6c5ce7;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 12px 20px;
  font-size: 16px;
  cursor: pointer;
  display: block;
  margin: 20px auto 0;
  width: 100%;
  transition: background-color 0.3s;
}

.login-btn:hover {
  background-color: #5649c0;
}
</style> 