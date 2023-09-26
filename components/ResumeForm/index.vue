<template>
    <div class="container">
        <div class="form-container">
            <el-tabs v-model="activeTab" class="tabs">
                <el-tab-pane label="Basics">
                    <BasicsForm v-model="formData.basics"/>
                </el-tab-pane>
                <el-tab-pane label="Work">
                    <WorkForm v-model="formData.work"/>
                </el-tab-pane>
                <el-tab-pane label="Education">
                    <EducationForm v-model="formData.education"/>
                </el-tab-pane>
                <el-tab-pane label="Certificates">
                    <CertificatesForm v-model="formData.certificates"/>
                </el-tab-pane>
                <el-tab-pane label="Skills">
                    <SkillsForm v-model="formData.skills"/>
                </el-tab-pane>
                <el-tab-pane label="Soft Skills">
                    <SoftSkillsForm v-model="formData.softSkills"/>
                </el-tab-pane>
                <el-tab-pane label="Interests">
                    <InterestsForm v-model="formData.interests"/>
                </el-tab-pane>
            </el-tabs>
            <div class="actions">
                <el-button type="primary" @click="submitForm">Submit</el-button>
            </div>
        </div>
        <div class="preview-container">
            <div class="actions">
                <el-button @click="copyToClipboard">Copy JSON</el-button>
            </div>
            <pre>{{ JSON.stringify(formData, null, 2) }}</pre>
        </div>
    </div>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import BasicsForm from './BasicsForm.vue';
import WorkForm from './WorkForm.vue';
import EducationForm from './EducationForm.vue';
import SkillsForm from './SkillsForm.vue';
import SoftSkillsForm from './SoftSkillsForm.vue';
import InterestsForm from './InterestsForm.vue';
import CertificatesForm from './CertificatesForm.vue';

const formData = ref({
    basics: {
        location: {},
    },
    work: [],
    education: [],
    certificates: [],
    skills: [],
    softSkills: [],
    interests: [],
    // Add more sections like projects, certificates, languages, etc. as needed
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
}

.form-container {
    flex-grow: 1;
    padding: 20px;
    display: flex;
    flex-direction: column;
}

.form-container .actions {
    padding-top: 20px;
    display: flex;
    justify-content: flex-start;
}

.tabs {
    height: 100%;
}

.preview-container {
    flex-grow: 1;
    background-color: #f5f5f5;
    padding: 10px;
    overflow: auto;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}


</style>
