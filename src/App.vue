<template>
	<!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
	<!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->

	<!-- <thing /> -->

	<force-chart />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Thing from './components/Thing.vue'
import ForceChart from './components/ForceChart.vue'

export default defineComponent({
	name: 'App',
	components: {
		HelloWorld,
		Thing,
		ForceChart
	}
})
</script>

<style>
body {
	margin: 0;
}
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
}
</style>