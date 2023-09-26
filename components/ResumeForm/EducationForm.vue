<template>
    <div>
        <div v-for="(edu, index) in education" :key="index" class="education-item">
            <el-form
                label-position="top"
                class="education-form"
                :model="edu"
                label-width="100px"
            >
                <el-form-item label="Institution">
                    <el-input v-model="edu.institution" @input="updateValue" placeholder="Institution" />
                </el-form-item>
                <el-form-item label="Area of Study">
                    <el-input v-model="edu.area" @input="updateValue" placeholder="Area of Study" />
                </el-form-item>
                <el-form-item label="Study Type">
                    <el-input v-model="edu.studyType" @input="updateValue" placeholder="Study Type" />
                </el-form-item>
                <el-form-item label="Location">
                    <el-input v-model="edu.location" @input="updateValue" placeholder="Location" />
                </el-form-item>
                <el-form-item label="Start Date">
                    <el-input v-model="edu.startDate" @input="updateValue" placeholder="Start Date" />
                </el-form-item>
                <el-form-item label="End Date">
                    <el-input v-model="edu.endDate" @input="updateValue" placeholder="End Date" />
                </el-form-item>
                <el-form-item label="Score">
                    <el-input v-model="edu.score" @input="updateValue" placeholder="Score" />
                </el-form-item>
                <el-form-item label="Courses">
                    <el-input v-model="edu.courses" @input="updateValue" placeholder="Courses" />
                </el-form-item>
                <el-form-item>
                    <el-button @click="removeEducation(index)" type="danger">Remove</el-button>
                </el-form-item>
            </el-form>
        </div>
        <el-button @click="addEducation" type="success" class="add-button">Add Education</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: {
        institution: string;
        area: string;
        studyType: string;
        location: string;
        startDate: string;
        endDate: string;
        score: string;
        courses: string[];
    }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const education = ref(
    props.modelValue.length
        ? props.modelValue
        : [
            {
                institution: '',
                area: '',
                studyType: '',
                location: '',
                startDate: '',
                endDate: '',
                score: '',
                courses: [],
            },
        ]
);

const addEducation = () => {
    education.value.push({
        institution: '',
        area: '',
        studyType: '',
        location: '',
        startDate: '',
        endDate: '',
        score: '',
        courses: [],
    });
    updateValue();
};

const removeEducation = (index: number) => {
    education.value.splice(index, 1);
    updateValue();
};

const updateValue = () => {
    emit('update:modelValue', education.value);
};
</script>

<style scoped>
.education-form {
    margin-bottom: 20px;
}

.add-button {
    margin-top: 10px;
}
</style>
