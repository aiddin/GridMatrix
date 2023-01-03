<template>
  <div>
    <table>
      <tr v-for="rows in rows" :key="rows">
       
        <td v-for="columns in columns" :key="columns"> <TcSparkline :sparklineData="sparklineData"/></td>
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
</template>

<script>
import TcSparkline from './TcSparkline.vue'
export default {
  components: {
    TcSparkline
  },
  data() {
    return {
      rows: 2,
      columns: 2,
      sparklineData: [936, 968, 1025, 999, 998, 1014, 1017, 1010, 1010, 1007,1113,1113],
    }
  },
  methods: {
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
  border: 1px solid black;
  border-collapse: collapse;
}

td {
  border: 5px solid rgb(255, 255, 255);
  background-color:  rgb(0, 0, 0);
  padding: 10px;
}
</style>