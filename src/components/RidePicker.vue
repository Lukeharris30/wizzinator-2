<script setup lang="ts">
import { defineModel, watch } from 'vue';
const mountainOrRoad = defineModel('mountainOrRoad')
watch(mountainOrRoad, (newval, oldval) =>{
    console.log('should be scrolling')
    const section = document.querySelector('section')
    section?.scrollIntoView({behavior: 'smooth'})
})
</script>

<template>
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
</template>

<style scoped>
.ride {
	display: flex;
	flex-direction: column;
	align-items: stretch;
	height: 60vh;
	width: 40vw;
	margin: auto;
	select {
		width: 100%;
		height: 50px;
		font-size: 20px;
	}
}
</style>