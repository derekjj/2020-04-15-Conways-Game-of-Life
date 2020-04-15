<template lang="pug">
  #app
    .container
      .row(v-for="(row, iRow) in world")
        div(v-for="(cell, iCol) in row" :key="iCol" @click="toggle(iRow,iCol)")
          div.border.p-3(:class="{'bg-primary' : cell,'bg-secondary' : !cell}")
</template>

<script>
import cell from "./components/cell.vue";
const ROW_SIZE = 30;
const COL_SIZE = 30;
export default {
  name: "App",
  components: {
    cell
  },
  data() {
    return {
      world: [],
      tempWord: []
    };
  },
  created() {
    this.initWorld(ROW_SIZE, COL_SIZE);
  },
  methods: {
    tick() {
      // times(ROW_SIZE);
    },
    initWorld(rowSize, colSize) {
      for (let rows = 0; rows < rowSize; rows++) {
        const row = [];
        for (let cols = 0; cols < colSize; cols++) {
          row.push(false);
        }
        this.world.push(row);
      }
    },
    times(iterations = 1, callback) {
      for (let i = 0; i < iterations; i++) {
        callback(i);
      }
    },
    toggle(cellRow, cellCol) {
      this.tempWord = this.world;
      this.tempWord[cellRow][cellCol] = !this.world[cellRow][cellCol];
      this.world = [];
      this.world = this.tempWord;
    },
    numNeighbours(cellRow, cellCol) {
      const startRow = cellRow - 1;
      const startCol = cellCol - 1;

      const endRow = cellRow + 1;
      const endCol = cellCol + 1;

      let numNeighbours = 0;
      console.log("startRow", startRow);
      console.log("startCol", startCol);
      console.log("endRow", endRow);
      console.log("endCol", endCol);

      for (let row = startRow; row < endRow; row++) {
        console.log("row", row);

        if (row < 0 || row > ROW_SIZE + 1) {
          continue;
        }
        for (var col = startCol; col < endCol; col++) {
          console.log("col", col);

          if (row === cellRow && col === cellCol) {
            continue;
          }
          if (this.world[row][col]) {
            numNeighbours++;
          }
        }
      }
      // console.log("ROW_SIZE", ROW_SIZE);
      // console.log("COL_SIZE", COL_SIZE);
      console.log("numNeighbours", numNeighbours);
      console.log();
      console.log("------------------------------");
      console.log();
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
