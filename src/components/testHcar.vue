<template>
    <table>
      <tr v-for="(row, rowIndex) in rows" :key="rowIndex">
        <td v-for="(cell, cellIndex) in row" :key="cellIndex" v-on:click="onCellClick">
          {{ cell }}
        </td>
      </tr>
    </table>
  </template>
  
  <script>
  export default {
    data() {
      return {
        rows: [],
      };
    },
    created() {
      // Generate rows and cells on the fly
      const rows = [];
      for (let rowIndex = 0; rowIndex < 10; rowIndex++) {
        const row = [];
        for (let cellIndex = 0; cellIndex < 10; cellIndex++) {
          row.push(`${rowIndex},${cellIndex}`);
        }
        rows.push(row);
      }
      this.rows = rows;
    },
    methods: {
      onCellClick(event) {
        const element = event.target;
        const parent = element.parentNode;
        const grandparent = parent.parentNode;
        const rows = grandparent.querySelectorAll('tr');
        const rowIndex = Array.prototype.indexOf.call(rows, parent);
        const cells = parent.querySelectorAll('td');
        const cellIndex = Array.prototype.indexOf.call(cells, element);
        console.log(`Row index: ${rowIndex}`);
        console.log(`Column index: ${cellIndex}`);
      },
    },
  };
  </script>