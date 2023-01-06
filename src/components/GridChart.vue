<template>
  <button @click="toggleDialog">Grid Chart </button>
  <window
  v-if="visible"
  :initial-width="300"
  :initial-height="300"
  :title="'Grid Chart'"
  :resizable="true"
  @close="toggleDialog"
  :style="{ height: '150px', cursor: 'default' }"
>
<div id="tblpck">
  <div>{{ hoverColumn }}X{{ hoverRow }} Table</div>
<table>
  <tr  v-for="(selectorrows, rowIndex) in selectorrows" :key="rowIndex">
    <td 
      v-for="selectorcolumns in selectorcolumns"
      :key="selectorcolumns"

      @mouseover="atasMouse($event)"
      @mouseenter="getCellIndex(rowIndex, selectorcolumns)"
      @click="handleCellClick($event)"
      
    ></td>
  </tr>
</table>
</div>
</window>

  <div >
    <br>

    <table class="huh" >
      <tr class="normal" v-for="(rows,rowIndex) in rows" :key="rowIndex">
        <div>
          <td class="normal" v-for="columns in columns" :key="columns" >
            <TcSparkline :sparklineData="sparklineData" />
          </td>
        </div>
      </tr>
    </table>
  </div>



  {{ selectedColumn }}
  {{ selectedRow }}

</template>
<script>
import TcSparkline from "./TcSparkline.vue";
import { Window } from "@progress/kendo-vue-dialogs";

import "hammerjs";
export default {
  components: {
    TcSparkline,
    window: Window,
  },
  data() {
    return {
      rowCount: 0,
      colCount: 0,
      visible: false,
      selectorrows: 10,
      selectorcolumns: 10,
      hoverColumn: 0,
      hoverRow: 0,
      rows: 2,
      columns: 2,
      sparklineData: [936, 968, 1025, 999, 998, 1014, 1017, 1010, 1010, 1007, 1113, 1113],
      selectedColumn: 3,
      selectedRow: 3,
    };
  },
  watch: {

    selectedColumn: {
      handler() {
        this.columns = this.selectedColumn;
      },
    },
    selectedRow: {
      handler() {
        this.rows = this.selectedRow;
      },
    },
  },

  methods: {
      atasMouse(e){
        if (e.target.tagName !== "TD") return;
            let td = e.target;
            let tr = td.parentNode;
            let table = tr.parentNode;
            this.colCount = td.cellIndex + 1;
            this.rowCount = tr.rowIndex + 1;
            for (let row of table.rows) {
              let inside = row.rowIndex < this.rowCount;
              for (let cell of row.cells) {
                cell.classList.toggle(
                  "tblpckhighlight",
                  inside && cell.cellIndex < this.colCount
                );

              }
              
            }
           
            return false;
      },
    getCellIndex(rowIndex, cellIndex) {
      this.hoverColumn = cellIndex;
      this.hoverRow = rowIndex+1;
      console.log(`Row index: ${rowIndex+1}`);
      console.log(`Cell index: ${cellIndex}`);
    },

    handleCellClick(event) {
      // Get the element that was clicked
      const element = event.target;
      // Get the row index
      const rowIndex = element.parentNode.rowIndex + 1;
      // Get the column index
      const cellIndex = element.cellIndex + 1;
      console.log(`Row index: ${rowIndex}, Column index: ${cellIndex}`);
      this.selectedColumn = cellIndex;
      this.selectedRow = rowIndex;
    },

    toggleDialog() {
      this.visible = !this.visible;
    },
  },
};
//table layout selected need to folow selectors
</script>
<style>

table.huh {
  border: 1px solid #000000;
}
table.selector{
  border: 1px solid #000000;
  width: 200px;
  height: 200px;
}

td{
  cursor: pointer;
  background-color: rgb(255, 255, 255);
  
  border: 1px solid #000000;
}
td:hover  {
  position: sticky;
  background-color: rgb(193, 74, 74);
}

tr {
  border-color: #000000;
  background-color: rgb(11, 215, 69);
}
tr:hover :nth-of-type(1){
  background-color: rgb(255, 255, 255);
  
} 
#tblpck div{background:#ccc;font-family:Verdana;text-align:right}
#tblpck table{border-spacing:3px;background:#f8f8f8}
#tblpck td{border:1px solid #888;width:16px;height:16px;box-sizing:border-box}
#tblpck .tblpckhighlight{border:2px solid orange;}
</style>
