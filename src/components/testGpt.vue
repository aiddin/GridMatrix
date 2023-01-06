<template>
    <div>
      <button @click="showTablePicker">Pick a table</button>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      async showTablePicker() {
        let [colCount, rowCount] = await this.tablePicker();
        console.log(JSON.stringify({ colCount, rowCount }));
      },
      tablePicker() {
        return new Promise(resolve => {
          let div = document.querySelector("#tblpck");
          if (div) div.remove();
          let colCount = 0;
          let rowCount = 0;
          div = document.createElement("div");
          div.setAttribute("id", "tblpck");
          div.innerHTML = `<style>
              #tblpck div{background:#ccc;font-family:Verdana;text-align:right}
              #tblpck table{border-spacing:3px;background:#f8f8f8}
              #tblpck td{border:1px solid #888;width:16px;height:16px;box-sizing:border-box}
              #tblpck .tblpckhighlight{border:2px solid orange;}
          </style><div>0x0 Table</div>
          <table>${`<tr>${`<td></td>`.repeat(10)}</tr>`.repeat(10)}</table>`;
          document.body.appendChild(div);
          Object.assign(div.style, {
            left: this.x + "px",
            top: this.y + "px",
            position: "absolute",
            border: "1px solid #ccc"
          });
  
          div.onmouseover = e => {
            if (e.target.tagName !== "TD") return;
            let td = e.target;
            let tr = td.parentNode;
            let table = tr.parentNode;
            colCount = td.cellIndex + 1;
            rowCount = tr.rowIndex + 1;
            for (let row of table.rows) {
              let inside = row.rowIndex < rowCount;
              for (let cell of row.cells) {
                cell.classList.toggle(
                  "tblpckhighlight",
                  inside && cell.cellIndex < colCount
                );
              }
            }
            div.children[1].textContent = `${colCount}x${rowCount} Table`;
            return false;
          };
  
          div.onmousedown = () => {
            div.remove();
            resolve([colCount, rowCount]);
          };
        });
      }
    }
  };
  </script>