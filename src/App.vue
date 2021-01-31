<template>
	<!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
	<!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->

	<!-- <thing /> -->

	<force-three />

	<packed-circle />
	<packed-circle-two />
	<packed-circle-three />
	<force-one />
	<force-two />
	<!-- <force-three /> -->
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import Thing from './components/Thing.vue'
import PackedCircle from './components/PackedCircle.vue'
import PackedCircleTwo from './components/PackedCircleTwo.vue'
import PackedCircleThree from './components/PackedCircleThree.vue'
import ForceOne from './components/ForceOne.vue'
import ForceTwo from './components/ForceTwo.vue'
import ForceThree from './components/ForceThree.vue'


export default defineComponent({
	name: 'App',
	components: {
		HelloWorld,
		Thing,
		PackedCircle,
		PackedCircleTwo,
		PackedCircleThree,
		ForceOne,
		ForceTwo,
		ForceThree
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