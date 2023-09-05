<script setup lang="ts">
import {ref, defineProps, defineEmits} from 'vue';

interface Props {
    modelValue: Record<string, any>;
}

const props = defineProps<Props>();
const emit = defineEmits();

const basics = ref(props.modelValue || {});

const updateValue = () => {
    emit('update:modelValue', basics.value);
};

</script>

<template>
    <div>
        <h2>Basics Information</h2>
        <input v-model="basics.name" @input="updateValue" placeholder="Name"/>
        <!-- Additional inputs -->
    </div>
</template>

<style scoped>
</style>
