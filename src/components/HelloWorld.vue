<template>
  <div>
    <table>
      <tr v-for="rows in rows" :key="rows">
       
        <td v-for="columns in columns" :key="columns">{{ column }}</td>
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
export default {
  data() {
    return {
      rows: 2,
      columns: 2
    }
  },
  methods: {
    addRow() {
      this.rows++
    },
    deleteRow() {
      if (this.rows > 1) {
        this.rows--
      }
    },
    addColumn() {
      this.columns++
    },
    deleteColumn() {
      if (this.columns > 1) {
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
  border: 1px solid black;
  padding: 8px;
}
</style>