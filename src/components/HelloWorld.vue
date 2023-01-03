<template>
  <form id="table-form">
    <label for="rows">Number of rows:</label>
    <input type="number" id="rows" v-model="rows">
    <br>
    <label for="columns">Number of columns:</label>
    <input type="number" id="columns" v-model="columns">
    <br>
    <button v-on:click.prevent="generateTable">Generate table</button>
  </form>
</template>
6785
<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return{
    rows: 0,
    columns: 0,
  };
  },
  computed: {
    tableData: function() {
      // Generate the table data based on the number of rows and columns
      var data = [];
      for (var i = 0; i < this.rows; i++) {
        var row = [];
        for (var j = 0; j < this.columns; j++) {
          row.push('');
        }
        data.push(row);
      }
      return data;
    }
  },
  methods: {
    generateTable: function() {
      // Generate the table using the table data
      var table = document.createElement('table');
      for (var i = 0; i < this.tableData.length; i++) {
        var row = document.createElement('tr');
        for (var j = 0; j < this.tableData[i].length; j++) {
          var cell = document.createElement('td');
          cell.textContent = this.tableData[i][j];
          row.appendChild(cell);
        }
        table.appendChild(row);
      }
      // Add the table to the page
      document.body.appendChild(table);
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
