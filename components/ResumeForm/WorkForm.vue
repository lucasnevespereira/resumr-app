<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { position: string, company: string }[];
}

const props = defineProps<Props>();
const emit = defineEmits();

// single empty work experience at first
const works = ref(props.modelValue.length ? props.modelValue : [{ position: '', company: '' }]);

const addWork = () => {
    works.value.push({ position: '', company: '' });
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

<template>
    <div>
        <h2>Work Experiences</h2>
        <div v-for="(work, index) in works" :key="index">
            <input v-model="work.position" @input="updateValue" placeholder="Position" />
            <input v-model="work.company" @input="updateValue" placeholder="Company" />
            <button @click="removeWork(Number(index))">Remove</button>
        </div>
        <button @click="addWork">Add Work Experience</button>
    </div>
</template>

<style scoped>
</style>
