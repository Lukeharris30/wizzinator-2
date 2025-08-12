<script setup lang="ts">
import { defineProps } from 'vue';
const props = defineProps({
    steps: Number,
    currentStep: {type: Number, required: true}
})
</script>
<template>
    <div class="steps-container">
        <TransitionGroup name="fadestep">
            <div v-for="(number, index) of props.steps" class="steps" :class="{selected: index === (props.currentStep -1)}" :key="index">{{currentStep > number ? '&#10003;' : index + 1}}</div>
        </TransitionGroup>
	</div>
</template>