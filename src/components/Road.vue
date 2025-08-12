<script setup lang="ts">
import { defineModel, defineProps } from 'vue';
import StepsContainer from './StepsContainer.vue';
import StepContent from './StepContent.vue';
const props = defineProps(
    {
        steps: Number,
        goingUp: Boolean,
        currentStep: {type:Number, required: true},
        OnexorTwox: String,
    }
)
const OnexorTwox = defineModel('OnexorTwox');

</script>
<template>
    <h1>Road</h1>
    <StepsContainer :steps="props.steps" :current-step="props.currentStep"/>
    <TransitionGroup :name="goingUp ? 'slide' : 'slideback'">
			<StepContent :step-number="1" :current-step="props.currentStep">
                <label>
                    One by or Two by?
                <select v-model="OnexorTwox">
                    <option value="1x"> 1x </option>
                    <option value="2x"> 2x</option>
                </select>
                </label>
            </StepContent>
            <StepContent :step-number="2" :current-step="props.currentStep">
                Another step
            </StepContent>
            <StepContent :step-number="3" :current-step="props.currentStep">
                almost last step
            </StepContent>
            <StepContent :step-number="4" :current-step="props.currentStep">
                Last step
            </StepContent>
        </TransitionGroup>
</template>