<template>
    <div>
        <h2>Basics Information</h2>
        <input v-model="basics.name" @input="updateValue" placeholder="Name"/>
        <input v-model="basics.label" @input="updateValue" placeholder="Job Title"/>
        <input v-model="basics.image" @input="updateValue" placeholder="Image URL"/>
        <input v-model="basics.email" @input="updateValue" placeholder="Email"/>
        <input v-model="basics.phone" @input="updateValue" placeholder="Phone"/>
        <div>
            <input v-model="basics.location.city" @input="updateValue" placeholder="City"/>
            <input v-model="basics.location.countryCode" @input="updateValue" placeholder="Country Code"/>
            <input v-model="basics.location.region" @input="updateValue" placeholder="Region"/>
        </div>
        <input v-model="basics.url" @input="updateValue" placeholder="Website URL"/>

        <div v-for="(profile, index) in basics.profiles" :key="index">
            <input v-model="profile.network" @input="updateProfile(index)" :placeholder="'Social ' + (index + 1) + ' Network'"/>
            <input v-model="profile.username" @input="updateProfile(index)" :placeholder="'Social ' + (index + 1) + ' Username'"/>
            <input v-model="profile.url" @input="updateProfile(index)" :placeholder="'Social ' + (index + 1) + ' URL'"/>
            <button @click="removeProfile(index)">Remove</button>
        </div>

        <button @click="addProfile">Add Social</button>
        <br />
        <textarea v-model="basics.summary" @input="updateValue" placeholder="Summary"></textarea>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: Record<string, any>;
}

const props = defineProps<Props>();
const emit = defineEmits();

const basics = ref(props.modelValue || {});

const updateValue = () => {
    emit('update:modelValue', basics.value);
};

const updateProfile = (index: number) => {
    emit('update:modelValue', basics.value);
};

const addProfile = () => {
    basics.value.profiles = basics.value.profiles || [];
    basics.value.profiles.push({ network: '', username: '', url: '' });
    emit('update:modelValue', basics.value);
};

const removeProfile = (index: number) => {
    basics.value.profiles.splice(index, 1);
    emit('update:modelValue', basics.value);
};
</script>

<style scoped>
</style>
