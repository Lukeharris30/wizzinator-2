<script setup lang="ts">
	import { ref, onMounted} from "vue"
	import Mountain from './components/Mountain.vue'
	import Road from './components/Road.vue'
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
	const udh = ref(false)
	const mountainOrRoad = ref('Road')
	const OnexorTwox = ref('')
</script>

<template>
  <div>
	<div class="ride">
		<div>
		<h1>Choose Road or Mountain</h1>
		</div>
		<div>
			<select v-model="mountainOrRoad">
				<option value="Road">Road</option>
				<option value="Mountain">Mountain</option>
			</select>
		</div>
	</div>
	<section>
		<div class="button-group">
			<Mountain v-if="mountainOrRoad === 'Mountain'" :steps="steps" :going-up="goingUp" :current-step="currentStep" v-model:udh="udh"></Mountain>
			<Road v-if="mountainOrRoad === 'Road'" :steps="steps" :going-up="goingUp" :currentStep="currentStep" v-model:OnexorTwox="OnexorTwox"></Road>
		   	<TransitionGroup name="fade">
				<button key="prev" class="prev" v-show="currentStep > 1" @click="previousStep">&#x2190;</button>
				<button key="next" class="next" v-show="currentStep < steps" @click="nextStep">&#x2192;</button>
			</TransitionGroup>
		</div>
	</section>
	<pre>
		udh{{udh}}
		oneBy? {{OnexorTwox }}
	</pre>
  </div>
</template>

<style >

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
.fadestep-enter-active, .fadestep-leave-active{
	transition: all .4s ease;
}
.fadestep-enter-from{
	background: #fff;
	color: black;
}
.fadestep-leave-to{
	background: #e51937;
	color: #fff;
}

.fade-enter-active, .fade-leave-active{
	transition: all .4s ease;
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
	    background: #e51937;
		color: #fff;
}
.steps:has(~ .selected){
	background: #e51937;
	color: #fff;
	&::after{
		content:'';
	
	}
}
.ride {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: space-between;
	height: 50vh;
	width: 40vw;
	margin: auto;
	select {
		width: 100%;
		height: 50px;
		font-size: 20px;
	}
}
</style>
