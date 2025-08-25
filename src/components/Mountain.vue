<script setup lang="ts">
import {defineProps, ref, defineModel, watch} from 'vue'
import StepsContainer from './StepsContainer.vue';
import StepContent from './StepContent.vue';
const props = defineProps(
    {
        steps: Number,
        goingUp: Boolean,
        currentStep: {type:Number, required: true},
        udh: Boolean,
    }
)
const udh = defineModel('udh')

</script>
<template>
    	<h1>Mountain</h1>
        <StepsContainer :steps="props.steps" :current-step="props.currentStep"/>
		<!-- steps -->
		<TransitionGroup :name="goingUp ? 'slide' : 'slideback'">
		<StepContent :step-number="1" :current-step="props.currentStep" key="1">
				<h2>UDH?</h2>
				<p>If your frame is UDH compatible, you can use Transmission, a direct mount to your bike frame.</p>
				<fieldset>
					My frame is UDH
				<label>yes<input id="udh_yes" value="yes" type="radio" v-model="udh"/></label>
				<label>no<input id="use_no" value="no" type="radio" v-model="udh"/></label>
				</fieldset>
				
		</StepContent>
		<StepContent :step-number="2" :current-step="props.currentStep" key="2">
			<h2>Mechanical or AXS?</h2>
			<p>We offer mechanichal shifting or electronic. Unsure which you want, <a href="https://sram.com">find out which is better for you.</a></p>
			<label>Mechanical<input type="radio" id="mechanical" value="mechanical"/></label>
			<label>Electronic (AXS)<input type="radio" id="Electronic" value="axs"/></label>
			
			
		</StepContent>
		<StepContent :step-number="3" :current-step="props.currentStep" key="3">
				Step three
		</StepContent>
		</TransitionGroup>
	
</template>
