<template>
	ForceChart:
	<br />

	<div class="svgSizer">
		<div class="svg-container">
			<svg viewBox="-400 -400 400 400">
				<!-- <circle cx="0" cy="0" r="400" fill="rgba(255, 0, 0, 0.25)" /> -->
				<circle
					v-for="(circ, i) in circles"
					:key="i"
					:cx="circ.x"
					:cy="circ.y"
					:r="circ.r"
					fill="rgba(255, 0, 0, 0.25)"
				/>
			</svg>
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import * as d3 from 'd3'

type Circ = {
	x: number,
	y: number,
	r: number
};

export default defineComponent({
	name: 'ForceChart',
	data() {
		return {
			circles: [] as Circ[]
		}
	},
	mounted() {
		console.log('ForceChart mounted');

		const random = d3.randomUniform(0, 100);
		console.log(random);

		const radii = d3.range(50).map(random);
		console.log(radii);

		const circles = d3.packSiblings(radii.map(r => ({ r })));
		console.log(circles);
		this.circles = circles;

		//   for (const circle of circles) {
		//     circle.x += width / 2;
		//     circle.y += height / 2;
		//     circle.r -= padding;
		//   }
		//   return circles;
	}
})
</script>

<style scoped>
.svgSizer {
	width: 400px;
	height: 400px;
	margin: 0 auto;
	border: thin solid pink;

	resize: both;
	overflow: auto; /* needed for resize to work */
}
.svg-container {
	display: inline-block;
	position: relative;
	width: 100%;
	height: 100%;
	/* padding-bottom: 100%; */
	vertical-align: middle;
	overflow: hidden;
}
.svg-container > svg {
	position: absolute;
	top: 0;
	left: 0;
	bottom: 0;
	right: 0;
	width: 100%;
	height: 100%;
}
</style>