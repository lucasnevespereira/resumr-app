<template>
    <div class="container">
        <div class="form-container">
            <el-tabs v-model="activeTab">
                <el-tab-pane label="Basics">
                    <BasicsForm v-model="formData.basics" />
                </el-tab-pane>
                <el-tab-pane label="Work">
                    <WorkForm v-model="formData.work" />
                </el-tab-pane>
                <!-- Add more tab panes for other sections like Education, etc. -->
            </el-tabs>
        </div>
        <div class="json-container">
            <div class="actions">
                <el-button @click="copyToClipboard">Copy JSON</el-button>
            </div>
            <pre>{{ JSON.stringify(formData, null, 2) }}</pre>
        </div>
    </div>
    <div class="actions">
        <el-button type="primary" @click="submitForm">Submit</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import BasicsForm from './BasicsForm.vue';
import WorkForm from './WorkForm.vue';

const formData = ref({
    basics: {
        location: {}
    },
    work: [],
    // Add more sections like education, skills, etc. as needed
});

const submitForm = () => {
    console.log('Submitted Form Data:', JSON.stringify(formData.value, null, 2));
};

const activeTab = ref('Basics');

const copyToClipboard = () => {
    const jsonText = JSON.stringify(formData.value, null, 2);
    navigator.clipboard.writeText(jsonText).then(() => {
        alert('JSON copied to clipboard');
    }).catch((error) => {
        console.error('Error copying JSON to clipboard:', error);
    });
};
</script>

<style scoped>
.container {
    display: flex;
    justify-content: space-between;
    padding: 20px; /* Add padding to provide space */
    gap: 20px;
}

.form-container {
    flex: 1;
    width: 70%; /* Adjust the width as needed */
}

.json-container {
    flex: 1;
    width: 25%; /* Adjust the width as needed */
    background: #f5f5f5;
    padding: 10px;
    overflow: auto;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.json-container .actions {
    display: flex;
    justify-content: flex-end;
}

.actions {
    padding: 20px;
    display: flex;
    justify-content: flex-start;
}

@media (max-width: 768px) {
    .container {
        flex-direction: column;
    }

    .form-container,
    .json-container {
        width: 100%; /* Use full width on smaller screens */
    }

    .json-container {
        margin-top: 20px;
    }
}
</style>
