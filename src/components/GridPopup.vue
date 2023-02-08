<template>
    <window
    v-if="visible"
    :initial-width="300"
    :initial-height="300"
    :title="'Grid Chart'"
    :resizable="true"
    :style="{ height: '150px', cursor: 'default' }"
  >
    <div id="tblpck">
      <div v-show="dimensionVisible">{{ hoverColumn }}X{{ hoverRow }} Table</div>
      <table>
        <tr v-for="(selectorrows, rowIndex) in selectorrows" :key="rowIndex">
          <td id="tblpck"
            v-for="selectorcolumns in selectorcolumns"
            :key="selectorcolumns"
            @mouseover="atasMouse($event)"
            @mouseenter="getCellIndex(rowIndex, selectorcolumns)"
            @click="handleCellClick($event),toggleDialog"
          ></td>
        </tr>
      </table>
    </div>
  </window>
</template>
<script>
import { Window } from "@progress/kendo-vue-dialogs";

import "hammerjs";
export default {
  props:["visible"],
  components: {
    
    window: Window,
  },
  data() {
    return {
      rowCount: 0,
      colCount: 0,
      
      selectorrows: 5,
      selectorcolumns: 5,
      dimensionVisible:  true,
      hoverColumn: 0,
      hoverRow: 0,
      rows: 3,
      columns: 3,
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
  computed: {
    tblpckStyle(){
      return {
        'huh': JSON.stringify(this.highlight),
      }
    },
  },
  methods: {
    atasMouse(e) {
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
      this.hoverRow = rowIndex + 1;
      console.log(`Row index: ${rowIndex + 1}`);
      console.log(`Cell index: ${cellIndex}`);
    },

    handleCellClick(event) {
      const element = event.target;
      const rowIndex = element.parentNode.rowIndex + 1;
      const cellIndex = element.cellIndex + 1;
      this.selectedColumn = cellIndex;
      this.selectedRow = rowIndex;
      this.toggleDialog();
    },

   
  },
};
//table layout selected need to folow selectors
</script>
<style scoped>
table.huh {
  border: 1px solid #000000;
}
table.selector {
  border: 1px solid #000000;
  width: 200px;
  height: 200px;
}
td {
  cursor: pointer;
  background-color: rgb(255, 255, 255);

  border: 1px solid #f4f4f4;
}
td:hover {
  position: sticky;
  background-color: rgb(193, 74, 74);
}
tr {
  border-color: #000000;
 
}
#tblpck div {
  background: rgb(255, 255, 255);
  font-family: Verdana;
  text-align: right;
}
#tblpck table {
  border-spacing: 3px;
  background: #ffffff;
}
#tblpck td {
  border: 1px solid #888;
  background-color: wheat;
  width: 16px;
  height: 16px;
  box-sizing: border-box;
}
#tblpck td:hover{
  background-color: red;
}
#tblpck .tblpckhighlight {
  border: 2px solid rgb(84, 58, 24);
}
</style>