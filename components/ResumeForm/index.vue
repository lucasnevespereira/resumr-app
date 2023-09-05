<script setup lang="ts">
import {ref} from 'vue';
import BasicsForm from './BasicsForm.vue';
import WorkForm from './WorkForm.vue';

const formData = ref({
    basics: {},
    work: [],
});

const submitForm = () => {
    console.log('Submitted Form Data:', JSON.stringify(formData.value, null, 2));
};
</script>

<template>
    <div class="container">
        <div class="form-container">
            <BasicsForm v-model="formData.basics"/>
            <WorkForm v-model="formData.work"/>
            <button @click="submitForm">Submit</button>
        </div>

        <div class="json-container">
            <pre>{{ JSON.stringify(formData, null, 2) }}</pre>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}

.form-container,
.json-container {
    flex: 1;
    min-width: calc(50% - 10px);
}

.json-container {
    background: #f5f5f5;
    padding: 10px;
    overflow: auto;
    height: 100vh;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

@media (max-width: 768px) {
    .container {
        flex-direction: column;
    }

    .form-container,
    .json-container {
        min-width: 100%;
    }

    .json-container {
        margin-top: 20px;
    }
}
</style>
