<script setup lang="ts">
	import { ref, onMounted} from "vue"
	const currentStep = ref(1);
	const goingUp = ref(true)
	function nextStep() {
		if(currentStep.value < steps.value){
			goingUp.value = true 
			currentStep.value ++;	
		}
	}
	function previousStep() {
		if(currentStep.value > 1){
			goingUp.value = false 
			currentStep.value --
		}
	}
	const steps = ref(0)
	onMounted(() => {
		steps.value = document.querySelectorAll('.step-content').length
	})
	// form data
	const udh = ref('')

</script>

<template>
  <div>
	<section>
		<h1>Mountain</h1>
		<div class="steps-container">
			<div v-for="(number, index) of steps" class="steps" :class="{selected: index === (currentStep -1)}" :key="index">{{currentStep > number ? '&#10003;' : index + 1}}</div>
		</div>
		<TransitionGroup :name="goingUp ? 'slide' : 'slideback'">
			<div v-show="currentStep === 1" key="1" class="step-content">
				<label>UDH?<input type="checkbox" v-model="udh"/></label>
			</div>
			<div v-show="currentStep === 2" key="2" class="step-content">
				Step two
			</div>
			<div v-show="currentStep === 3" key="3" class="step-content">
				Step three
			</div>
		</TransitionGroup>
		<div class="button-group">
		   	<TransitionGroup name="fade">
				<button key="prev" class="prev" v-show="currentStep > 1" @click="previousStep">&#x2190;</button>
				<button key="next" class="next" v-show="currentStep < steps" @click="nextStep">&#x2192;</button>
			</TransitionGroup>
		</div>
	</section>
	<pre>udh{{udh}}</pre>
  </div>
</template>

<style scoped>

section {
	margin: auto;
	text-align: center;
	width: 40vw;
}
.step-content{
	display: flex;
	align-items: center;
	justify-content: center;
	min-height: 200px;
}
.button-group {
	position: relative;
	button {
		position: absolute;
		width: 40px;
		background: transparent;
		padding: 4px 10px;
	}
	button.next {
		position: absolute;
		right: 0;
	}
	button.prev {
		left: 0;
	}
}
.fade-enter-active, .fade-leave-active{
	transition: opacity .4s ease;
}
.fade-leave-active{
	position: absolute;
}
.fade-enter-from{
	opacity: 0;
}
.fade-leave-to{
	opacity: 0;
}
.slide-enter-active, .slide-leave-active{
	transition: all 1s ease;
}
.slide-leave-active {
	position: absolute;
	display: none;
}
.slide-enter-from {
	transform: translateX(40px);
	opacity: 0;
}
.slide-leave-to {
	transform: translateX(40px);
	opacity: 0;
}
.slideback-enter-active, .slideback-leave-active{
	transition: all 1s ease;
}
.slideback-leave-active {
	position: absolute;
	display: none;
}
.slideback-enter-from {
	transform: translateX(-40px);
	opacity: 0;
}
.slideback-leave-to {
	transform: translateX(-40px);
	opacity: 0;
}
.steps-container {
	width: 100%;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}
.steps {
      width: 30px;
      height: 30px;
      border: 1px solid black;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
}
.selected {
	    background: #eee;
}
.steps:has(~ .selected){
	background: red;
	&::after{
		content:'';
	
	}
}

</style>
