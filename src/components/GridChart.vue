<template>
  <div>
    <table>
      <tr v-for="rows in rows" :key="rows">
       <div>
        <td v-for="columns in columns" :key="columns"> <TcSparkline :sparklineData="sparklineData"/></td>
      </div>
      </tr>
    </table>  
  </div>
  <div>
    <table>
      <tr v-for="(selectorrows,rowIndex) in selectorrows" :key="rowIndex">
        <td v-for="selectorcolumns in selectorcolumns" :key="selectorcolumns" @click="handleCellClick"></td>
      </tr>
    </table>
  </div>
  {{selectedColumn}}
  {{selectedRow}}
</template>

<script>
import TcSparkline from './TcSparkline.vue'
import "hammerjs"; 
export default {
  components: {
    TcSparkline
  },
  data() {
    return {
      selectorrows: 10,
      selectorcolumns: 10,
      rows: 2,
      columns: 2,
      sparklineData: [936, 968, 1025, 999, 998, 1014, 1017, 1010, 1010, 1007,1113,1113],
      selectedColumn:2,
      selectedRow:2,
    }
  },
  watch: {
    selectedColumn:{ handler() {
        this.columns=this.selectedColumn;

      }
    },
    selectedRow:{ handler() {
        this.rows=this.selectedRow;

      }
    }
  },
  methods: {
    handleCellClick(event) {
      // Get the element that was clicked
      const element = event.target;
      // Get the row index
      const rowIndex = element.parentNode.rowIndex+1;
      // Get the column index
      const cellIndex = element.cellIndex+1;
      console.log(`Row index: ${rowIndex}, Column index: ${cellIndex}`);
      this.selectedColumn=(cellIndex);
      this.selectedRow=(rowIndex);
    },
    addRow() {
      this.rows++
    },
    deleteRow() {
      if (this.rows > 0) {
        this.rows--
      }
    },
    addColumn() {
      this.columns++
    },
    deleteColumn() {
      if (this.columns > 0) {
        this.columns--
      }
    }
  }
}
</script>

<style>
table {
  border: 1px solid rgb(255, 1, 1);
 
}

td {
  border: 1vw solid rgb(7, 7, 7);
 cursor: pointer;
  background-color:  rgb(0, 0, 0);
  
}
 tr{
  border: 5px solid rgb(255, 255, 255);
  background-color:  rgb(0, 0, 0);
 }
</style>
 