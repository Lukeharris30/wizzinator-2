<script setup lang="ts">
import {defineProps, ref, defineModel, watch} from 'vue'
import StepsContainer from './StepsContainer.vue';
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
			<div v-show="currentStep === 1" key="1" class="step-content">
			<fieldset>
				<h2>UDH?</h2>
				<p>If your frame is UDH compatible, you can use Transmission, a direct mount to your bike frame.</p>
				<fieldset>
					My frame is UDH
				<label>yes<input id="udh" type="checkbox" v-model="udh"/></label>
				<label>no<input id="udh" type="checkbox" v-model="udh"/></label>
				</fieldset>
			</fieldset>
				
			</div>
			<div v-show="currentStep === 2" key="2" class="step-content">
				Step two
			</div>
			<div v-show="currentStep === 3" key="3" class="step-content">
				Step three
			</div>
		</TransitionGroup>
	
</template>
