<template>
	<div>
		<div class="flex flex-col">
			<div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
				<div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
					<div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
						<table class="min-w-full divide-y divide-gray-200">
							<thead class="bg-gray-50">
								<tr>
									<th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider" v-for="(c, ci) in table[0]" :key="ci">
										<div class="flex">
											<span>
												<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 mr-2" @click="addColumn(ci)" title="add column">
													<svg class="h-2 w-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
														<path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
													</svg>
												</button>	
											</span>
											<input type="text" v-model="table[0][ci]" class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block min-w-min w-full sm:text-sm border-gray-300 rounded-md" :title="table[0][ci]" />
											<span>
												<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 ml-2" @click="removeColumn(ci)" title="remove column">
													<svg xmlns="http://www.w3.org/2000/svg" class="h-2 w-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
														<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 12H4" />
													</svg>
												</button>
											</span>
											<span>
												<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 ml-2" v-if="ci === table[0].length - 1" @click="addColumn(ci + 1)" title="add column">
													<svg class="h-2 w-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
														<path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
													</svg>
												</button>
											</span>
										</div>
									</th>
									<th>
										<div class="flex">
											<span class="mr-2">Actions</span>
											<span>
												<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 mr-2" @click="addRow(-1)" title="add row above">
													<svg class="h-2 w-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
														<path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
													</svg>
												</button>	
											</span>
											<span>
												<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 mr-2" @click="removeRow(0)" title="remove row">
													<svg xmlns="http://www.w3.org/2000/svg" class="h-2 w-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
														<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 12H4" />
													</svg>
												</button>
											</span>
											<span>
												<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500" @click="addRow(1)" title="add row below">
													<svg class="h-2 w-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
														<path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
													</svg>
												</button>
											</span>
										</div>
									</th>
								</tr>
							</thead>
							<tbody>
								<tr class="" v-for="(r, ri) in table" :key="ri" :class="{'hidden': ri == 0, 'bg-white': ri % 2, 'bg-gray-50' : !(ri % 2)}">
									<td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900" v-for="(c, ci) in table[ri]" :key="ci">
										<input type="text" v-model="table[ri][ci]" class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md" :title="table[ri][ci]">
									</td>
									<td>
										<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 mr-2" v-if="ri === 0" @click="addRow(-1)" title="add row before">
											<svg class="h-2 w-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
												<path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
											</svg>
										</button>
										<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 mr-2" @click="removeRow(ri)" title="remove row">
											<svg xmlns="http://www.w3.org/2000/svg" class="h-2 w-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 12H4" />
											</svg>
										</button>
										<button type="button" class="inline-flex items-center p-1 border border-transparent rounded-full shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500" @click="addRow(ri)" title="add row after">
											<svg class="h-2 w-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
												<path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
											</svg>
										</button>
									</td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>
		<button @click="exportTable" class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 mt-2">Export table</button>
	</div>
</template>

<script>
export default {
	name: 'TableEditor',
	props: ['propTable'],
	data() {
		return {
			table: [['new column']]
		}
	},
	created() {
		this.$nextTick(() => {
			this.table = this.propTable
		})
	},
	methods: {
		addColumn(index) {
			this.table.map(row => {
				row.splice(index, 0, '')
			})
		},
		removeColumn(index) {
			console.log(index)
			this.table.map(row => {
				row.splice(index, 1)
			})
			if (this.table[0].length == 0) {
				this.table = [['new column']]
			}
		},
		addRow(index) {
			let cols = this.table[0].length
			let newRow = []
			while (cols > 0) {
				newRow.push('')
				cols--
			}
			if (index === -1) {
				this.table.unshift(newRow)
			} else {
				this.table.splice(index + 1, 0, newRow)
			}
			console.log(index)
		},
		removeRow(index) {
			this.table.splice(index, 1)
			if (this.table.length === 0) {
				this.table = [['new column']]
			}
		},
		exportTable() {
			this.$emit('export', this.table)
		}
	}
}
</script>