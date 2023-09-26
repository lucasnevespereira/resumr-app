<template>
    <div>
        <el-form label-position="top" :model="basics">
            <el-form-item label="Name">
                <el-input v-model="basics.name" @input="updateValue" placeholder="Name"></el-input>
            </el-form-item>
            <el-form-item label="Job Title">
                <el-input v-model="basics.label" @input="updateValue" placeholder="Job Title"></el-input>
            </el-form-item>
            <el-form-item label="Image URL">
                <el-input v-model="basics.image" @input="updateValue" placeholder="Image URL"></el-input>
            </el-form-item>
            <el-form-item label="Email">
                <el-input v-model="basics.email" @input="updateValue" placeholder="Email"></el-input>
            </el-form-item>
            <el-form-item label="Phone">
                <el-input v-model="basics.phone" @input="updateValue" placeholder="Phone"></el-input>
            </el-form-item>
            <el-form-item label="Location">
                <el-input v-model="basics.location.city" @input="updateValue" placeholder="City"></el-input>
                <el-input v-model="basics.location.countryCode" @input="updateValue"
                          placeholder="Country Code"></el-input>
                <el-input v-model="basics.location.region" @input="updateValue" placeholder="Region"></el-input>
            </el-form-item>
            <el-form-item label="Website URL">
                <el-input v-model="basics.url" @input="updateValue" placeholder="Website URL"></el-input>
            </el-form-item>

            <el-form-item label="Socials">
                <div v-for="(profile, index) in basics.profiles" :key="index">
                    <el-input v-model="profile.network" @input="updateProfile(Number(index))"
                              :placeholder="'Social  Network'"></el-input>
                    <el-input v-model="profile.username" @input="updateProfile(Number(index))"
                              :placeholder="'Social Username'"></el-input>
                    <el-input v-model="profile.url" @input="updateProfile(Number(index))"
                              :placeholder="'Social URL'"></el-input>
                    <el-button type="danger" @click="removeProfile(Number(index))">Remove</el-button>
                </div>
            </el-form-item>

            <el-form-item>
                <el-button @click="addProfile">Add Social</el-button>
            </el-form-item>

            <el-form-item label="Summary">
                <el-input v-model="basics.summary" @input="updateValue" type="textarea"
                          placeholder="Summary"></el-input>
            </el-form-item>
        </el-form>
    </div>
</template>

<script setup lang="ts">
import {ref, defineProps, defineEmits} from 'vue';

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
    emit('update:modelValue', basics.value);
};

const addProfile = () => {
    basics.value.profiles = basics.value.profiles || [];
    basics.value.profiles.push({network: '', username: '', url: ''});
    emit('update:modelValue', basics.value);
};

const removeProfile = (index: number) => {
    basics.value.profiles.splice(index, 1);
    emit('update:modelValue', basics.value);
};
</script>
