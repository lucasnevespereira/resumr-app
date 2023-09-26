<template>
    <div>
        <h2>Certificates</h2>
        <div v-for="(certificate, index) in certificates" :key="index" class="certificate-item">
            <el-row :gutter="10">
                <el-col :span="8">
                    <el-input v-model="certificate.title" @input="updateValue" placeholder="Title"></el-input>
                </el-col>
                <el-col :span="4">
                    <el-input v-model="certificate.date" @input="updateValue" placeholder="Date"></el-input>
                </el-col>
                <el-col :span="6">
                    <el-input v-model="certificate.issuer" @input="updateValue" placeholder="Issuer"></el-input>
                </el-col>
                <el-col :span="4">
                    <el-input v-model="certificate.score" @input="updateValue" placeholder="Score"></el-input>
                </el-col>
                <el-col :span="8">
                    <el-input v-model="certificate.url" @input="updateValue" placeholder="URL"></el-input>
                </el-col>
                <el-col :span="2">
                    <el-button @click="removeCertificate(index)" type="danger">Remove</el-button>
                </el-col>
            </el-row>
        </div>
        <el-button @click="addCertificate" type="success" class="add-button">Add Certificate</el-button>
    </div>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue';

interface Props {
    modelValue: { title: string; date: string; issuer: string; score: string; url: string }[];
}

const props = defineProps<Props>();
const emit = defineEmits<{}>();

const certificates = ref(
    props.modelValue.length
        ? props.modelValue
        : [{ title: '', date: '', issuer: '', score: '', url: '' }]
);

const addCertificate = () => {
    certificates.value.push({ title: '', date: '', issuer: '', score: '', url: '' });
    updateValue();
};

const removeCertificate = (index: number) => {
    certificates.value.splice(index, 1);
    updateValue();
};

const updateValue = () => {
    emit('update:modelValue', certificates.value);
};
</script>
