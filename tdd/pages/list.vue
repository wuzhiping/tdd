<template>
  <div style="height:100%;">
    <div style=" height: calc(60% - 5px);">
      <ag-grid-vue
        style="zoom:115%;"
        id="grid"
        class="ag-theme-balham"
        ref="grid"
        :default-col-def="defaultColDef"
        :column-defs="columnDefs"
        :row-data="rowData"
        :grid-options="gridOptions"
      ></ag-grid-vue>
    </div>
  </div>
</template>

<script>
module.exports = {
  components: {
    AgGridVue: window["ag-grid-vue"].AgGridVue
  },
  data() {
    return {
      defaultColDef: {
        menuTabs: [],
        width: 100,
        sortable: false,
        resizable: true
      },
      rowData: [
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" },
        { aa: "aa1", bb: "bb1", cc: "cc1", dd: "dd1" },
        { aa: "aa2", bb: "bb2", cc: "cc2", dd: "dd2" },
        { aa: "aa3", bb: "bb3", cc: "cc3", dd: "dd3" }
      ],
      gridOptions: {},
      columnDefs: null
    };
  },
  watch: {},
  methods: {},
  created: function() {
    this.$store.commit("error", "请先保存表单");
  },
  mounted: function() {
    this.columnDefs = [
      {
        headerName: "aa",
        field: "aa",
        //pinned: "left",
        editable: true,
        singleClickEdit: true,
        cellEditor: "agRichSelectCellEditor",
        cellEditorParams: {
          values: ["aa1", "aa2", "aa3"]
        }
      },
      {
        headerName: "bb",
        field: "bb"
      },
      {
        headerName: "cc",
        field: "cc",
        width: 250
      },
      {
        headerName: "dd",
        field: "dd"
      }
    ];
  }
};
</script>

<style scoped>
.ag-cell-edit-input option {
  font-size: 130% !important;
}
</style>
