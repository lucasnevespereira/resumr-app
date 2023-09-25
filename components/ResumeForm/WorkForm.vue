<template>
    <div>
      <h2>Work Experiences</h2>
      <div v-for="(work, index) in works" :key="index" class="work-item">
        <div class="work-inputs">
          <input v-model="work.position" @input="updateValue" placeholder="Position" />
          <input v-model="work.company" @input="updateValue" placeholder="Company" />
          <input v-model="work.startDate" @input="updateValue" placeholder="Start Date (e.g., Jan 2020)" />
          <input v-model="work.endDate" @input="updateValue" placeholder="End Date (e.g., Dec 2022)" />
          <textarea v-model="work.summary" @input="updateValue" placeholder="Summary"></textarea>
        </div>
        <button @click="removeWork(index)" class="remove-button">Remove</button>
      </div>
      <button @click="addWork" class="add-button">Add Work Experience</button>
    </div>
</template>
  
  <script setup lang="ts">
  import { ref, defineProps, defineEmits } from 'vue';
  
  interface Props {
    modelValue: { position: string; company: string; startDate: string; endDate: string; summary: string }[];
  }
  
  const props = defineProps<Props>();
  const emit = defineEmits();
  
  const works = ref(
    props.modelValue.length
      ? props.modelValue
      : [{ position: '', company: '', startDate: '', endDate: '', summary: '' }]
  );
  
  const addWork = () => {
    works.value.push({ position: '', company: '', startDate: '', endDate: '', summary: '' });
    updateValue();
  };
  
  const removeWork = (index: number) => {
    works.value.splice(index, 1);
    updateValue();
  };
  
  const updateValue = () => {
    emit('update:modelValue', works.value);
  };
  </script>
  
  <style scoped>
  .work-item {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .work-inputs {
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    margin-right: 10px;
  }
  
  .remove-button {
    background-color: #ff6b6b;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  
  .add-button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    margin-top: 10px;
  }
  
  .add-button:hover {
    background-color: #45a049;
  }
  
  .remove-button:hover {
    background-color: #ff4136;
  }
  </style>
  