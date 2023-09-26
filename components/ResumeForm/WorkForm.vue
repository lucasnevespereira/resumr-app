<template>
    <div>
        <h2>Work Experiences</h2>
        <div v-for="(work, index) in works" :key="index" class="work-item">
            <el-row :gutter="10">
                <el-col :span="6">
                    <el-input v-model="work.position" @input="updateValue" placeholder="Position"></el-input>
                </el-col>
                <el-col :span="6">
                    <el-input v-model="work.company" @input="updateValue" placeholder="Company"></el-input>
                </el-col>
                <el-col :span="4">
                    <el-input v-model="work.startDate" @input="updateValue" placeholder="Start Date (e.g., Jan 2020)"></el-input>
                </el-col>
                <el-col :span="4">
                    <el-input v-model="work.endDate" @input="updateValue" placeholder="End Date (e.g., Dec 2022)"></el-input>
                </el-col>
                <el-col :span="4">
                    <el-input v-model="work.summary" @input="updateValue" placeholder="Summary"></el-input>
                </el-col>
                <el-col :span="2">
                    <el-button @click="removeWork(index)" type="danger">Remove</el-button>
                </el-col>
            </el-row>
        </div>
        <el-button @click="addWork" type="success" class="add-button">Add Work Experience</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { position: string; company: string; startDate: string; endDate: string; summary: string }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

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
/* You can add scoped styles here if needed */
</style>
