<script setup lang="ts">
import {defineProps} from 'vue'
const props = defineProps({
    stepNumber: {type: Number, required: true},
    currentStep: {type: Number, required: true}
})
</script>
<template>
    <div v-show="props.currentStep === props.stepNumber" :key="props.stepNumber" class="step-content">
        <slot>
        </slot>
    </div>
</template>