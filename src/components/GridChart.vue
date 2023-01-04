<template>
  <div>
    <table>
      <tr v-for="rows in rows" :key="rows">
       <div>
        <td v-for="columns in columns" :key="columns"> <TcSparkline :sparklineData="sparklineData"/></td>
      </div>
      </tr>
    </table>
    <br>
    <label>Rows:</label>
    <input type="number" v-model="rows">
    <br>
    <label>Columns:</label>
    <input type="number" v-model="columns">
    <br>
    <button @click="addRow">Add Row</button>
    <button @click="deleteRow">Delete Row</button>
    <button @click="addColumn">Add Column</button>
    <button @click="deleteColumn">Delete Column</button>
  </div>
  <div>
    <table>
      <tr v-for="selectorrows in selectorrows" :key="selectorrows">
       <div>
        <td v-for="selectorcolumns in selectorcolumns" :key="selectorcolumns"></td>
      </div>
      </tr>
    </table>
  </div>
  <div>
    <table>
      <tr v-for="(row, rowIndex) in rows" :key="rowIndex">
        <td v-for="(cell, cellIndex) in row" :key="cellIndex" @click="handleCellClick">{{ cell }}</td>
      </tr>
    </table>
  </div>
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
      row: [
        ['A1', 'A2', 'A3'],
        ['B1', 'B2', 'B3'],
        ['C1', 'C2', 'C3']
      ]
    }
  },
  methods: {
    handleCellClick(event) {
      // Get the element that was clicked
      const element = event.target;
      // Get the row index
      const rowIndex = element.parentNode.rowIndex;
      // Get the column index
      const cellIndex = element.cellIndex;
      console.log(`Row index: ${rowIndex}, Column index: ${cellIndex}`);
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
  border: 5px solid rgb(255, 255, 255);
 cursor: pointer;
  background-color:  rgb(0, 0, 0);
  
}
 tr{
  border: 5px solid rgb(255, 255, 255);
  background-color:  rgb(0, 0, 0);
 }
</style>
 