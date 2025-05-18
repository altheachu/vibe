<script setup>
// No props or state needed for this simple component
</script>

<template>
  <div class="success-card">
    <div class="success-icon">✓</div>
    <h2>問卷已成功送出</h2>
    <p>謝謝您的填寫，我們會盡快處理您的資料。</p>
  </div>
</template>

<style scoped>
.success-card {
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  padding: 30px;
  max-width: 400px;
  width: 100%;
  text-align: center;
}

.success-icon {
  font-size: 60px;
  color: #00b894;
  margin-bottom: 15px;
  height: 80px;
  width: 80px;
  background-color: #e7f9f4;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px;
}

h2 {
  color: #6c5ce7;
  margin-bottom: 15px;
  font-size: 1.8rem;
}

p {
  color: #636e72;
  font-size: 16px;
}
</style> 