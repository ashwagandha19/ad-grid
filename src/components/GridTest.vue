<template>
<div>
  <h1>Grid</h1>
  <button @click="getSelectedRows()">Get Selected Rows</button>
  <ag-grid-vue
    style="width: 1000px; height: 500px"
    class="ag-theme-material"
    :columnDefs="columnDefs"
    :rowData="rowData"
    rowSelection="multiple"
    @grid-ready = "onGridReady"
    :autoGroupColumnDef = "autoGroupColumnDef"
  >
  </ag-grid-vue>
</div>
</template>

<script>
import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-material.css";
import { AgGridVue } from "ag-grid-vue";

export default {
  data() {
    return {
      columnDefs: null,
      rowData: null,
      gridApi: null,
      columnApi: null,
      autoGroupColumnDef: null
    };
  },
  components: {
    AgGridVue,
  },
  methods: {
    getSelectedRows() {
            const selectedNodes = this.gridApi.getSelectedNodes();
            const selectedData = selectedNodes.map(node => node.data);
            const selectedDataStringPresentation = selectedData.map(node => node.id + ' ' + node.name).join(', ');
            alert(`Selected nodes: ${selectedDataStringPresentation}`);
    },
    onGridReady(params) {
            this.gridApi = params.api;
            this.columnApi = params.columnApi;
    },
  },
  beforeMount() {
    this.columnDefs = [
        // row group: true => drowpdown
    { field: 'id', sortable: true, filter: true, rowGroup: true },
    { field: 'name', sortable: true, filter: true },
    { field: 'username', sortable: true, filter: true },
    { field: 'email', sortable: true, filter: true },
    ];

    this.rowData = [];

    fetch('https://jsonplaceholder.typicode.com/users')
             .then(result => result.json())
             .then(rowData => this.rowData = rowData)
             .catch(err => console.log(err));     

    this.autoGroupColumnDef = {
        headerName: 'id',
        field: 'id',
        cellRenderer: 'agGroupCellRenderer',
        cellRendererParams: {
            checkbox: true
        }
    }

  },


};
</script>

<style>
   @import "~ag-grid-community/dist/styles/ag-grid.css";
   @import "~ag-grid-community/dist/styles/ag-theme-alpine.css";
</style>