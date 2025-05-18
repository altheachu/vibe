<script setup>
import { ref } from 'vue';
import RegistrationPage from './components/RegistrationPage.vue';
import QuestionnaireFlow from './components/QuestionnaireFlow.vue';

// Navigator state
const activeTab = ref('registration'); // 'registration' or 'questionnaire'

// Reference to the questionnaire flow component
const questionnaireFlowRef = ref(null);

// Handle tab switching
const switchTab = (tab) => {
  activeTab.value = tab;
};

// Handle C123 case (need registration)
const handleNeedRegistration = () => {
  alert('請先掛號');
  activeTab.value = 'registration';
};
</script>

<template>
  <main>
    <div class="container">
      <!-- Tab Navigator -->
      <div class="tab-navigator">
        <button 
          class="tab-button" 
          :class="{ active: activeTab === 'registration' }"
          @click="switchTab('registration')"
        >
          掛號
        </button>
        <button 
          class="tab-button" 
          :class="{ active: activeTab === 'questionnaire' }"
          @click="switchTab('questionnaire')"
        >
          診前問卷
        </button>
      </div>
      
      <!-- Tab Content -->
      <div class="tab-content">
        <!-- Registration Tab -->
        <RegistrationPage v-if="activeTab === 'registration'" />
        
        <!-- Questionnaire Tab -->
        <QuestionnaireFlow 
          v-if="activeTab === 'questionnaire'" 
          ref="questionnaireFlowRef"
          @need-registration="handleNeedRegistration" 
        />
      </div>
    </div>
  </main>
</template>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

body {
  background-color: #f5f6fa;
}

.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.tab-navigator {
  display: flex;
  width: 100%;
  max-width: 600px;
  margin-bottom: 20px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}

.tab-button {
  flex: 1;
  padding: 12px;
  background-color: #f1f2f6;
  border: none;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s;
}

.tab-button.active {
  background-color: #6c5ce7;
  color: white;
}

.tab-content {
  width: 100%;
  display: flex;
  justify-content: center;
}

@media (min-width: 768px) {
  .tab-content {
    max-width: 800px;
  }
}
</style>
