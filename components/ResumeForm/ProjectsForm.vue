<template>
    <div>
        <h2>Projects</h2>
        <div v-for="(project, index) in projects" :key="index" class="project-item">
            <el-row :gutter="10">
                <el-col :span="6">
                    <el-input v-model="project.name" @input="updateValue" placeholder="Project Name"></el-input>
                </el-col>
                <el-col :span="12">
                    <el-input v-model="project.description" @input="updateValue" placeholder="Project Description"></el-input>
                </el-col>
                <el-col :span="6">
                    <el-input v-model="project.url" @input="updateValue" placeholder="Project URL"></el-input>
                </el-col>
                <el-col :span="2">
                    <el-button @click="removeProject(index)" type="danger">Remove</el-button>
                </el-col>
            </el-row>
        </div>
        <el-button @click="addProject" type="success" class="add-button">Add Project</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { name: string; description: string; url: string }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const projects = ref(
    props.modelValue.length
        ? props.modelValue
        : [{ name: '', description: '', url: '' }]
);

const addProject = () => {
    projects.value.push({ name: '', description: '', url: '' });
    updateValue();
};

const removeProject = (index: number) => {
    projects.value.splice(index, 1);
    updateValue();
};

const updateValue = () => {
    emit('update:modelValue', projects.value);
};
</script>