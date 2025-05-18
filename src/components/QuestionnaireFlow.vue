<script setup>
import { ref, defineEmits } from 'vue';
import LoginPage from './LoginPage.vue';
import QuestionnaireComponent from './QuestionnaireComponent.vue';
import SuccessPage from './SuccessPage.vue';

// Define sample questions
const questionnaireA = {
  title: '情緒與壓力評估表',
  questions: [
    '請描述您最近一週的情緒狀態',
    '您通常如何處理壓力？',
    '您如何評價自己的睡眠品質？'
  ]
};

const questionnaireB = {
  title: '人際關係評估表',
  questions: [
    '您如何描述您的社交圈？',
    '您在人際關係中遇到的最大挑戰是什麼？',
    '您在與他人溝通時感到舒適嗎？'
  ]
};

// Component state
const currentPage = ref('login'); // 'login', 'questionnaireA', 'questionnaireB', 'success'
const userId = ref('');

// Answers state
const answersA = ref([]);
const answersB = ref([]);

// Define emit for special handling of C123
const emit = defineEmits(['needRegistration']);

// Handle login
const handleLogin = (data) => {
  userId.value = data.id;
  
  if (data.id === 'C123') {
    // Special case for C123
    emit('needRegistration');
    return;
  } else if (data.id === 'A123') {
    currentPage.value = 'questionnaireA';
  } else if (data.id === 'B123') {
    currentPage.value = 'questionnaireB';
  } else {
    alert('無效的ID，請使用A123或B123');
  }
};

// Handle questionnaire submission
const handleSubmit = () => {
  // Validation for questionnaire A
  if (currentPage.value === 'questionnaireA') {
    const isCompleteA = answersA.value.every(answer => answer && answer.trim() !== '') && 
                         answersA.value.length === questionnaireA.questions.length;
    const isCompleteB = answersB.value.every(answer => answer && answer.trim() !== '') && 
                         answersB.value.length === questionnaireB.questions.length;
    
    if (!isCompleteA || !isCompleteB) {
      alert('請填寫所有問題');
      return;
    }
  }
  
  // Validation for questionnaire B
  if (currentPage.value === 'questionnaireB') {
    const isComplete = answersB.value.every(answer => answer && answer.trim() !== '') && 
                         answersB.value.length === questionnaireB.questions.length;
    
    if (!isComplete) {
      alert('請填寫所有問題');
      return;
    }
  }
  
  currentPage.value = 'success';
};

// Handle return to home
const returnToHome = () => {
  currentPage.value = 'login';
  userId.value = '';
  answersA.value = [];
  answersB.value = [];
};

// Reset the flow
const resetFlow = () => {
  currentPage.value = 'login';
  userId.value = '';
  answersA.value = [];
  answersB.value = [];
};

// Expose the reset method to the parent
defineExpose({
  resetFlow
});
</script>

<template>
  <div class="questionnaire-flow">
    <!-- Login Page -->
    <LoginPage 
      v-if="currentPage === 'login'"
      @login="handleLogin"
    />
    
    <!-- Questionnaire A Page (Both components) -->
    <div v-if="currentPage === 'questionnaireA'" class="questionnaires">
      <QuestionnaireComponent
        :title="questionnaireA.title"
        :questions="questionnaireA.questions"
        @update:answers="answersA = $event"
      />
      <QuestionnaireComponent
        :title="questionnaireB.title"
        :questions="questionnaireB.questions"
        @update:answers="answersB = $event"
      />
      <button @click="handleSubmit" class="submit-btn">確認送出</button>
    </div>
    
    <!-- Questionnaire B Page (Only component B) -->
    <div v-if="currentPage === 'questionnaireB'" class="questionnaires">
      <QuestionnaireComponent
        :title="questionnaireB.title"
        :questions="questionnaireB.questions"
        @update:answers="answersB = $event"
      />
      <button @click="handleSubmit" class="submit-btn">確認送出</button>
    </div>
    
    <!-- Success Page -->
    <div v-if="currentPage === 'success'" class="success-container">
      <SuccessPage />
      <button @click="returnToHome" class="return-btn">返回首頁</button>
    </div>
  </div>
</template>

<style scoped>
.questionnaire-flow {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.questionnaires {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  width: 100%;
}

.submit-btn {
  background-color: #6c5ce7;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  display: block;
  margin: 20px auto 0;
  transition: background-color 0.3s;
  max-width: 600px;
  width: 100%;
}

.submit-btn:hover {
  background-color: #5649c0;
}

.return-btn {
  background-color: #6c5ce7;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  display: block;
  margin: 20px auto 0;
  transition: background-color 0.3s;
  max-width: 400px;
  width: 100%;
}

.return-btn:hover {
  background-color: #5649c0;
}

.success-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  width: 100%;
}

@media (min-width: 768px) {
  .questionnaires {
    max-width: 800px;
  }
}
</style> 