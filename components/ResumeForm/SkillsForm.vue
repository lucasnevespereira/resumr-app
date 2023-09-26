<template>
    <div>
        <h2>Skills</h2>
        <div v-for="(skill, index) in skills" :key="index" class="skill-item">
            <el-row :gutter="10">
                <el-col :span="10">
                    <el-input v-model="skill.name" @input="updateValue" placeholder="Skill Name"></el-input>
                </el-col>
                <el-col :span="6">
                    <el-input v-model="skill.level" @input="updateValue" placeholder="Skill Level"></el-input>
                </el-col>
                <el-col :span="8">
                    <el-input v-model="skill.keywords" @input="updateValue" placeholder="Keywords (Comma Separated)"></el-input>
                </el-col>
                <el-col :span="2">
                    <el-button @click="removeSkill(index)" type="danger">Remove</el-button>
                </el-col>
            </el-row>
        </div>
        <el-button @click="addSkill" type="success" class="add-button">Add Skill</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { name: string; level: string; keywords: string[] }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const skills = ref(
    props.modelValue.length
        ? props.modelValue
        : [{ name: '', level: '', keywords: [] }]
);

const addSkill = () => {
    skills.value.push({ name: '', level: '', keywords: [] });
    updateValue();
};

const removeSkill = (index: number) => {
    skills.value.splice(index, 1);
    updateValue();
};

const updateValue = () => {
    emit('update:modelValue', skills.value);
};
</script>
