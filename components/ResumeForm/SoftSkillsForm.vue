<template>
    <div>
        <h2>Soft Skills</h2>
        <div v-for="(softSkill, index) in softSkills" :key="index" class="soft-skill-item">
            <el-row :gutter="10">
                <el-col :span="10">
                    <el-input v-model="softSkill.name" @input="updateValue" placeholder="Soft Skill Name"></el-input>
                </el-col>
                <el-col :span="2">
                    <el-button @click="removeSoftSkill(index)" type="danger">Remove</el-button>
                </el-col>
            </el-row>
        </div>
        <el-button @click="addSoftSkill" type="success" class="add-button">Add Soft Skill</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { name: string }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const softSkills = ref(
    props.modelValue.length
        ? props.modelValue
        : [{ name: '' }]
);

const addSoftSkill = () => {
    softSkills.value.push({ name: '' });
    updateValue();
};

const removeSoftSkill = (index: number) => {
    softSkills.value.splice(index, 1);
    updateValue();
};

const updateValue = () => {
    emit('update:modelValue', softSkills.value);
};
</script>

