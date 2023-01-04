<template>
  <div >
    <table>
      <tr v-for="rows in rows" :key="rows">
        <div>
          <td v-for="columns in columns" :key="columns" @click="toggleDialog">
            <TcSparkline :sparklineData="sparklineData" />
          </td>
        </div>
      </tr>
    </table>
  </div>
  <window
    v-if="visible"
    :initial-width="auto"
    :initial-height="auto"
    :title="'Grid Chart'"
    :resizable="true"
    @close="toggleDialog"
    :style="{ height: '150px', cursor: 'default' }"
  >
    <div>
      <table>
        <tr v-for="(selectorrows, rowIndex) in selectorrows" :key="rowIndex">
          <td
            v-for="selectorcolumns in selectorcolumns"
            :key="selectorcolumns"
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
      selectorrows: 10,
      selectorcolumns: 10,
      rows: 2,
      columns: 2,
      sparklineData: [936, 968, 1025, 999, 998, 1014, 1017, 1010, 1010, 1007, 1113, 1113],
      selectedColumn: 2,
      selectedRow: 2,
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
</script>

<style>
table {
  border: auto solid rgb(255, 1, 1);
}

td {
  border: 1vw solid rgb(7, 7, 7);
  cursor: pointer;
  background-color: rgb(0, 0, 0);
}
tr {
  border: 1vw solid rgb(255, 255, 255);
  background-color: rgb(0, 0, 0);
}
</style>
