<template>
	<div>
		<textarea v-text="textileTable" class="overflow-x-auto w-full font-mono whitespace-nowrap" rows="30" @click="$event.target.select()" />
	</div>
</template>

<script>
export default {
	name: 'ExportTable',
	props: ['propTable'],
	data() {
		return {
			table: [['new column']]
		}
	},
	computed: {
		textileTable() {
			let longest = []
			const columnCount = this.table[0].length
			for (let i = 0; i < columnCount; i++) {
				let lengths = this.table.map((row, ri) => {
					if (ri === 0) {
						return row[i].length + 3	
					}
					return row[i].length
				})
				longest.push(Math.max(...lengths))
			}
			return this.table.map((r, ri) => {
				return '| ' + r.map((c, ci) => {
					return ((ri == 0 ? '_. ' : '') + c).padEnd(longest[ci])
				}).join(' | ') + ' |'
			}).join('\n')
		}
	},
	created() {
		this.$nextTick(() => {
			this.table = this.propTable
		})
	}
}
</script>