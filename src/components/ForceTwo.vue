<template>
	ForceTwo:
	<br />

	<div class="svgSizer">
		<div class="svg-container">
			<svg :viewBox="`0 0 ${size} ${size}`">
				<circle
					v-for="(node, i) in nodes"
					:key="i"
					:cx="node.x"
					:cy="node.y"
					:r="node.radius"
					fill="rgba(0, 0, 255, 0.25)"
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
	name: 'ForceTwo',
	data() {
		return {
			size: 400, // px (kind of)
			padding: 5, // px

			radii: [] as number[],

			// nodes: [{}, {}, {}, {}, {}] as any[],
			nodes: d3.range(100).map(function (d) {
				return { radius: Math.random() * 25 }
			}) as any[],

			simulation: {} as any
		}
	},
	computed: {
		// circles(): Circ[] {
		// 	const circles = d3.packSiblings(this.radii.map(r => ({ r })));
		// 	for (const circle of circles) {
		// 		circle.x += this.size / 2;
		// 		circle.y += this.size / 2;
		// 		circle.r -= this.padding;
		// 		circle.r = Math.max(circle.r, 0); // keeps r from being negative (but some dont show becuase of this)
		// 	}
		// 	return circles;
		// }
	},
	mounted() {
		console.log('ForceTwo mounted');

		this.simulation = d3.forceSimulation(this.nodes)
			.force('charge', d3.forceManyBody().strength(5))
			.force('center', d3.forceCenter(this.size / 2, this.size / 2))
			.force('collision', d3.forceCollide().radius((d: any) => d.radius))
	},
	methods: {}
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