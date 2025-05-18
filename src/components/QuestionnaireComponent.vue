<script setup>
import { ref } from 'vue';

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  questions: {
    type: Array,
    required: true
  }
});

const answers = ref(props.questions.map(() => ''));

const emit = defineEmits(['update:answers']);

// Track answers and emit them to parent
const updateAnswer = (index, value) => {
  answers.value[index] = value;
  emit('update:answers', answers.value);
};
</script>

<template>
  <div class="questionnaire-card">
    <h2>{{ title }}</h2>
    
    <div v-for="(question, index) in questions" :key="index" class="question-item">
      <p>{{ index + 1 }}. {{ question }}</p>
      <textarea
        v-model="answers[index]"
        @input="updateAnswer(index, answers[index])"
        rows="3"
        :placeholder="`請輸入您的回答...`"
      ></textarea>
    </div>
  </div>
</template>

<style scoped>
.questionnaire-card {
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
  max-width: 600px;
  width: 100%;
}

h2 {
  color: #6c5ce7;
  text-align: center;
  margin-bottom: 20px;
  font-size: 1.5rem;
}

.question-item {
  margin-bottom: 15px;
}

p {
  margin-bottom: 5px;
  font-weight: 500;
}

textarea {
  width: 100%;
  padding: 10px;
  border: 2px solid #dfe6e9;
  border-radius: 8px;
  font-size: 14px;
  transition: border-color 0.3s;
}

textarea:focus {
  border-color: #6c5ce7;
  outline: none;
}
</style> 