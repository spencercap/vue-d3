<template>
	PackedCircleThree:
	<br />

	<div class="svgSizer">
		<div class="svg-container">
			<svg :viewBox="`0 0 ${size} ${size}`">
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
	name: 'PackedCircleThree',
	data() {
		return {
			size: 1200, // px (kind of)
			padding: 5, // px
			radii: [] as number[],
		}
	},
	computed: {
		circles(): Circ[] {
			const circles = d3.packSiblings(this.radii.map(r => ({ r })));
			for (const circle of circles) {
				circle.x += this.size / 2;
				circle.y += this.size / 2;
				circle.r -= this.padding;
				circle.r = Math.max(circle.r, 0); // keeps r from being negative (but some dont show becuase of this)
			}
			return circles;
		}
	},
	mounted() {
		console.log('PackedCircleThree mounted');

		// const random = this.getRandom;
		const random = d3.randomUniform(0, 100);
		// console.log(random);

		const radii = d3.range(50).map(random);
		// console.log(radii);
		this.radii = radii;
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