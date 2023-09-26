<template>
    <div>
        <el-form label-position="top" v-for="(work, index) in works" :key="index" class="work-item">
            <el-form-item label="Position">
                <el-input v-model="work.position" @input="updateValue" placeholder="Position"></el-input>
            </el-form-item>
            <el-form-item label="Company">
                <el-input v-model="work.company" @input="updateValue" placeholder="Company"></el-input>
            </el-form-item>
            <el-form-item label="Start Date (e.g., Jan 2020)">
                <el-input v-model="work.startDate" @input="updateValue" placeholder="Start Date"></el-input>
            </el-form-item>
            <el-form-item label="End Date (e.g., Dec 2022)">
                <el-input v-model="work.endDate" @input="updateValue" placeholder="End Date"></el-input>
            </el-form-item>
            <el-form-item label="Summary">
                <el-input v-model="work.summary" @input="updateValue" placeholder="Summary"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button @click="removeWork(index)" type="danger">Remove</el-button>
            </el-form-item>
        </el-form>
        <el-button @click="addWork" class="add-button">Add Work Experience</el-button>
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

