<template>
  <div id="app" class="container mx-auto mt-5">
    <div class="bg-white overflow-hidden shadow rounded-lg">
      <div class="px-4 py-5 sm:p-6">
        <stepper :step="step" @step="updateStep" class="mb-5" />
        <editor v-if="step == 1" @parsed="proceedToEdit" />
        <table-editor v-if="step == 2" :prop-table="table" @export="proceedToExport" />
        <export-table v-if="step == 3" :prop-table="table" />
      </div>
    </div>
  </div>
</template>

<script>
import Editor from './components/Editor'
import ExportTable from './components/ExportTable'
import Stepper from './components/Stepper'
import TableEditor from './components/TableEditor'
export default {
  name: 'App',
  components: {
    Editor,
    ExportTable,
    Stepper,
    TableEditor
  },
  data() {
    return {
      step: 1,
      textile: '',
      table: [['new column']]
    }
  },
  methods: {
    updateStep(step) {
      this.step = step
    },
    proceedToEdit(table) {
      this.$nextTick(() => {
        this.table = table
        this.step = 2
      })
    },
    proceedToExport(table) {
      this.$nextTick(() => {
        this.table = table
        this.step = 3
      })
    }
  }
}
</script>