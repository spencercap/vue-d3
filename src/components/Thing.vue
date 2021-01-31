<template>
	Thing
	{{ hello }}
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
	name: 'Thing',
	data() {
		return {
			hello: 'world'
		}
	}
})
</script>

<style scoped>
</style>