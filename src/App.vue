<script setup lang="ts">
	import { ref } from "vue"
	const currentStep = ref(1);
	function nextStep() {
		currentStep.value ++;	
	}
	function previousStep() {
		if(currentStep.value > 1){
			currentStep.value --
		}
	}

</script>

<template>
  <div>

	<section>
		<TransitionGroup name="slide">
		<div v-if="currentStep === 1" class="step-content">Step one</div>
		<div v-if="currentStep === 2" class="step-content">Step two</div>
		<div v-if="currentStep === 3" class="step-content">Step three</div>
		</TransitionGroup>
		<div class="button-group">
		   <transition name="fade">
		   <button v-show="currentStep > 1" @click="previousStep">&#x2190;</button>
		   </transition>
		   <button class="next" @click="nextStep">&#x2192;</button>
		</div>
	</section>

  </div>
</template>

<style scoped>
section {
	margin: auto;
	text-align: center;
	width: 300px;
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
		left: 0;
		width: 40px;
	}
	button.next {
		position: absolute;
		right: 0;
	}
}
.fade-enter-active, .fade-leave-active{
	transition: opacity 1s ease;
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
</style>
