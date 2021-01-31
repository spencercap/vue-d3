<template>
	ForceOne:
	<br />

	<div class="svgSizer">
		<div class="svg-container">
			<svg :viewBox="`0 0 ${size} ${size}`">
				<circle
					v-for="(node, i) in nodes"
					:key="i"
					:cx="node.x"
					:cy="node.y"
					:r="`20`"
					fill="rgba(0, 255, 0, 0.75)"
				/>

				<!-- <circle
					v-for="(circ, i) in circles"
					:key="i"
					:cx="circ.x"
					:cy="circ.y"
					:r="circ.r"
					fill="rgba(255, 0, 0, 0.25)"
				/> -->
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
	name: 'ForceOne',
	data() {
		return {
			size: 1200, // px (kind of)
			padding: 5, // px

			radii: [] as number[],

			nodes: [{}, {}, {}, {}, {}] as any[],
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
		console.log('ForceOne mounted');

		this.simulation = d3.forceSimulation(this.nodes)
			.force('charge', d3.forceManyBody())
			.force('center', d3.forceCenter(this.size / 2, this.size / 2))
		// .on('tick', this.ticked);
	},
	methods: {
		ticked() {
			// var u = d3.select('svg')
			// 	.selectAll('circle')
			// 	.data(this.nodes)

			// u.enter()
			// 	.append('circle')
			// 	.attr('r', 5)
			// 	.merge(u)
			// 	.attr('cx', function (d) {
			// 		return d.x
			// 	})
			// 	.attr('cy', function (d) {
			// 		return d.y
			// 	})

			// u.exit().remove()

			// this.nodes
		}
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