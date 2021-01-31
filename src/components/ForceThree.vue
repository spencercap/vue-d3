<template>
	ForceThree:
	<br />

	<div class="svgSizer">
		<div class="svg-container">
			<svg :viewBox="`0 0 ${size} ${size}`">
				<line
					v-for="(link, i) in graph.links"
					:key="i"
					:x1="link.source.x"
					:y1="link.source.y"
					:x2="link.target.x"
					:y2="link.target.y"
					class="link"
				/>
				<circle
					v-for="(node, i) in graph.nodes"
					:key="i"
					:cx="node.x"
					:cy="node.y"
					:r="`12`"
					:class="`node ${node.fixed ? 'fixed' : ''}`"
					@mousedown="(node.dragging = true), (node.fixed = true)"
					@mousemove="dragged($event, node)"
					@mouseup="resetDragging(node)"
					@mouseleave="resetDragging(node)"
					@click="clicked($event, node)"
				/>
			</svg>
		</div>
	</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import * as d3 from 'd3'

// example ported for vue from:
// https://observablehq.com/@d3/sticky-force-layout?collection=@d3/d3-force

type Nodely = d3.SimulationNodeDatum & { dragging?: boolean, fixed?: boolean };

export default defineComponent({
	name: 'ForceThree',
	data() {
		return {
			size: 400, // px (kind of)
			padding: 5, // px
			simulation: {} as any,

			graph: {
				nodes: Array.from({ length: 13 }, () => ({})) as Nodely[],
				links: [
					{ source: 0, target: 1 },
					{ source: 1, target: 2 },
					{ source: 2, target: 0 },
					{ source: 1, target: 3 },
					{ source: 3, target: 2 },
					{ source: 3, target: 4 },
					{ source: 4, target: 5 },
					{ source: 5, target: 6 },
					{ source: 5, target: 7 },
					{ source: 6, target: 7 },
					{ source: 6, target: 8 },
					{ source: 7, target: 8 },
					{ source: 9, target: 4 },
					{ source: 9, target: 11 },
					{ source: 9, target: 10 },
					{ source: 10, target: 11 },
					{ source: 11, target: 12 },
					{ source: 12, target: 10 }
				] as any[]
				// ] as d3.Line[]
			}
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
		console.log('ForceThree mounted');

		this.simulation = d3
			.forceSimulation()
			.nodes(this.graph.nodes)
			.force("charge", d3.forceManyBody())
			.force('center', d3.forceCenter(this.size / 2, this.size / 2))
			.force("link", d3.forceLink(this.graph.links))
	},
	methods: {
		dragged(event: MouseEvent, node: Nodely) {
			// console.log('dragged', event, node);
			if (!node.dragging) return; // only do shit if its dragged w mousedown

			node.fx = this.clamp(event.offsetX, 0, this.size);
			node.fy = this.clamp(event.offsetY, 0, this.size);
			this.simulation.alpha(1).restart();
		},
		clamp(x: number, lo: number, hi: number): number {
			return x < lo ? lo : x > hi ? hi : x;
		},
		clicked(event: MouseEvent, node: Nodely) {
			if (!node.fixed) return;
			if (node.dragging) return;

			delete node.fx;
			delete node.fy;
			node.fixed = false;
			this.simulation.alpha(1).restart();
		},
		// debounce dragend so click doesnt fire correctly
		resetDragging(node: Nodely) {
			setTimeout(() => {
				node.dragging = false;
			}, 100);
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

.link {
	stroke: #000;
	stroke-width: 1.5px;
}

.node {
	cursor: move;
	fill: #ccc;
	stroke: #000;
	stroke-width: 1.5px;
}

.node.fixed {
	fill: #f00;
}
</style>