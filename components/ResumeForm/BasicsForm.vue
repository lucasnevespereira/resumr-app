<template>
    <div>
        <h2>Basics Information</h2>

        <el-input v-model="basics.name" @input="updateValue" placeholder="Name"></el-input>
        <el-input v-model="basics.label" @input="updateValue" placeholder="Job Title"></el-input>
        <el-input v-model="basics.image" @input="updateValue" placeholder="Image URL"></el-input>
        <el-input v-model="basics.email" @input="updateValue" placeholder="Email"></el-input>
        <el-input v-model="basics.phone" @input="updateValue" placeholder="Phone"></el-input>
        <div>
            <el-input v-model="basics.location.city" @input="updateValue" placeholder="City"></el-input>
            <el-input v-model="basics.location.countryCode" @input="updateValue" placeholder="Country Code"></el-input>
            <el-input v-model="basics.location.region" @input="updateValue" placeholder="Region"></el-input>
        </div>
        <el-input v-model="basics.url" @input="updateValue" placeholder="Website URL"></el-input>

        <div v-for="(profile, index) in basics.profiles" :key="index">
            <el-input v-model="profile.network" @input="updateProfile(index)" :placeholder="'Social ' + (index + 1) + ' Network'"></el-input>
            <el-input v-model="profile.username" @input="updateProfile(index)" :placeholder="'Social ' + (index + 1) + ' Username'"></el-input>
            <el-input v-model="profile.url" @input="updateProfile(index)" :placeholder="'Social ' + (index + 1) + ' URL'"></el-input>
            <el-button @click="removeProfile(index)">Remove</el-button>
        </div>

        <el-button @click="addProfile">Add Social</el-button>
        <br />
        <el-input v-model="basics.summary" @input="updateValue" type="textarea" placeholder="Summary"></el-input>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: Record<string, any>;
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const basics = ref(props.modelValue || {});

const updateValue = () => {
    emit('update:modelValue', basics.value);
};

const updateProfile = (index: number) => {
    this.emit('update:modelValue', basics.value);
};

const addProfile = () => {
    basics.value.profiles = basics.value.profiles || [];
    basics.value.profiles.push({ network: '', username: '', url: '' });
    this.emit('update:modelValue', basics.value);
};

const removeProfile = (index: number) => {
    basics.value.profiles.splice(index, 1);
    this.emit('update:modelValue', basics.value);
};
</script>

<style scoped>
</style>
