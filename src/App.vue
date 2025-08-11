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
		<TransitionGroup name="slide"/>
		<div v-if="currentStep === 1">Step one</div>
		<div v-if="currentStep === 2">Step two</div>
		</TransitionGroup>
		<transition name="fade">
		<button v-if="currentStep > 1" @click="previousStep">Previous</button>
		</transition>
		<button @click="nextStep">Next</button>
	</section>

  </div>
</template>

<style scoped>
.fade-enter-active, .fade-leave-active{
	transition: opacity 2s ease;
}
.fade-enter-from{
	opacity: 0;
}
.fade-leave-to{
	opacity: 0;
}
.slide-enter-active, .slide-leave-active{
	transition: all 2s ease;
}
.slide-leave-active {
	position: absolute;
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
