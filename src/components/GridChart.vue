<template>
  <button @click="toggleDialog">Grid Chart</button>
<GridPopup v-if="visible" @close="toggleDialog" />
  <div>   
    <br />
    <table class="huh">
      <tr class="normal" v-for="(rows, rowIndex) in rows" :key="rowIndex">
        <div>
          <td class="normal" v-for="columns in columns" :key="columns">
            <TcSparkline :sparklineData="sparklineData" />
          </td>
        </div>
      </tr>
    </table>
  </div>
</template>
<script>
import TcSparkline from "./TcSparkline.vue";
import GridPopup from "./GridPopup.vue";
import "hammerjs";
export default {
  props:["row","column","isVisible","highlight","cellColor","endPoint"],
  components: {
    TcSparkline,
    GridPopup
  },
  data() {
    return {
      rowCount: 0,
      colCount: 0,
      visible: false,
      selectorrows: this.row,
      selectorcolumns: this.column,
      dimensionVisible:  this.isVisible,
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

    toggleDialog() {
      this.visible = !this.visible;
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
  background-color: v-bind(cellColor);
  width: 16px;
  height: 16px;
  box-sizing: border-box;
}
#tblpck td:hover{
  background-color: v-bind(endPoint);
}
#tblpck .tblpckhighlight {
  border: 2px solid v-bind(highlight);
}
</style>
