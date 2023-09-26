<template>
    <div>
        <h2>Interests</h2>
        <div v-for="(interest, index) in interests" :key="index" class="interest-item">
            <el-row :gutter="10">
                <el-col :span="10">
                    <el-input v-model="interest.name" @input="updateValue" placeholder="Interest Name"></el-input>
                </el-col>
                <el-col :span="2">
                    <el-button @click="removeInterest(index)" type="danger">Remove</el-button>
                </el-col>
            </el-row>
        </div>
        <el-button @click="addInterest" type="success" class="add-button">Add Interest</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { name: string }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const interests = ref(
    props.modelValue.length
        ? props.modelValue
        : [{ name: '' }]
);

const addInterest = () => {
    interests.value.push({ name: '' });
    updateValue();
};

const removeInterest = (index: number) => {
    interests.value.splice(index, 1);
    updateValue();
};

const updateValue = () => {
    emit('update:modelValue', interests.value);
};
</script>
