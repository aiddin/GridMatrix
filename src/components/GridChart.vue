<template>
  <button @click="toggleDialog">window</button>

  <div >
    <br>

    <table >
      <tr v-for="(rows,rowIndex) in rows" :key="rowIndex">
        <div>
          <td class="normal" v-for="columns in columns" :key="columns" >
            <TcSparkline :sparklineData="sparklineData" />
          </td>
        </div>
      </tr>
    </table>
  </div>



  <window
    v-if="visible"
    :initial-width="300"
    :initial-height="300"
    :title="'Grid Chart'"
    :resizable="true"
    @close="toggleDialog"
    :style="{ height: '150px', cursor: 'default' }"
  >
    <div>
    
      <table class="normal">
        <tr class="normal" v-for="(selectorrows, rowIndex) in selectorrows" :key="rowIndex">
          <td class="normal"
            v-for="selectorcolumns in selectorcolumns"
            :key="selectorcolumns"
            @mouseover="getCellIndex(rowIndex, selectorcolumns)"
            @click="handleCellClick"
            
          ></td>
        </tr>
      </table>
    </div>
  </window>
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
      visible: false,
      selectorrows: 5,
      selectorcolumns: 5,
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
    getCellIndex(rowIndex, cellIndex) {
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
.test {
 
  border: 1px solid #000000;
  width: 200px;
  height: 100px;
  object-fit: scale-down;
}


table {
  table-layout: fixed;
  width: 200px;
  height: 200px;
  border: 1px solid #000000;
}


td{

  cursor: pointer;
  background-color: rgb(154, 22, 22);
}
td.normal :hover  {


  background-color: rgb(143, 52, 255);
}

tr.normal {
  
  background-color: rgb(11, 215, 69);
}
tr.normal :hover {
  
  background-color: rgb(255, 255, 255);
}
</style>
