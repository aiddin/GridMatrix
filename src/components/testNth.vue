<template>
    <table>
      <tr v-for="row in rows" :key="row.id">
        <td v-for="cell in row.cells" :key="cell.id" @mouseenter="highlightCells(cell.id, $event)" @mouseleave="unhighlightCells(cell.id, $event)">
          {{ cell.value }}
        </td>
      </tr>
    </table>
  </template>
  <script>
  export default {
    data() {
      return {
        rows: [
          {
            id: 1,
            cells: [
              { id: 1, value: 'A1' },
              { id: 2, value: 'B1' },
              { id: 3, value: 'C1' },
              { id: 4, value: 'D1' }
            ]
          },
          {
            id: 2,
            cells: [
              { id: 5, value: 'A2' },
              { id: 6, value: 'B2' },
              { id: 7, value: 'C2' },
              { id: 8, value: 'D2' }
            ]
          }
        ]
      }
    },
    methods: {
      highlightCells(cellId, event) {
        // Get the cell that was hovered
        const hoveredCell = event.target;
        // Get the index of the hovered cell
        const cellIndex = hoveredCell.cellIndex;
        // Get all the cells in the same row as the hovered cell
        const cellsInRow = hoveredCell.parentElement.cells;
        // Highlight all the cells in the row by setting their background color
        for (let i = 0; i < cellsInRow.length; i++) {
          cellsInRow[i].style.backgroundColor = '#f1f1f1';
        }
      },
      unhighlightCells(cellId, event) {
        // Get the cell that was hovered
        const hoveredCell = event.target;
        // Get the index of the hovered cell
        const cellIndex = hoveredCell.cellIndex;
        // Get all the cells in the same row as the hovered cell
        const cellsInRow = hoveredCell.parentElement.cells;
        // Unhighlight all the cells in the row by setting their background color back to the default
        for (let i = 0; i < cellsInRow.length; i++) {
          cellsInRow[i].style.backgroundColor = '';
        }
      }
    }
  }
  </script>`