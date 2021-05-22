<template>
	<div class="lg:border-t lg:border-b lg:border-gray-200">
		<nav class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8" aria-label="Progress">
			<ol class="rounded-md overflow-hidden lg:flex lg:border-l lg:border-r lg:border-gray-200 lg:rounded-none">
				<step title="Load table" description="Insert textile table to start with" step="1" :current-step="step" @step="bubbleStep" :separator="false" />
				<step title="Modify table" description="Add or remove columns and rows" step="2" :current-step="step" @step="bubbleStep" :separator="true" />
				<step title="Export table" description="Create new textile markup" step="3" :current-step="step"  @step="bubbleStep" :separator="true" />
			</ol>
		</nav>
	</div>
</template>

<script>
import Step from './Step'
export default {
	name: 'Stepper',
	props: ['step'],
	components: {
		Step
	},
	methods: {
		bubbleStep(step) {
			this.$emit('step', step)
		}
	}
}
</script>