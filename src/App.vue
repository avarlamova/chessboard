<template>
  <!-- <Board @dragover="allowDrop" @drop="onDrop" /> -->
  <div @dragover="allowDrop" @drop="onDrop">
    <div v-for="row in 8" :key="row" class="row">
      <div v-for="col in 8" :key="col">
        <Cell
          @drop="onDrop($event, row, col)"
          @onDraggedElement="handleDrag"
          :computed-class="getCellClass(row, col)"
          :row="row"
          :col="col"
          :white-rook-position="whiteRookPosition"
          :black-rook-position="blackRookPosition"
        />
      </div>
    </div>
  </div>
</template>

<script>
// import Board from "./components/Board.vue";
// import Rook from "./components/Rook.vue";
import Cell from "./components/Cell.vue";

// import Castle from "./components/Castle.vue";
export default {
  name: "App",
  components: {
    // Board,
    // Rook,
    Cell,
  },
  data() {
    return {
      rooks: [
        { id: "1", color: "white", col: 1, row: 1 },
        { id: "2", color: "black" },
      ],
      draggedElement: {},
      whiteRookPosition: {
        col: 1,
        row: 1,
      },
      blackRookPosition: {
        col: 1,
        row: 8,
      },
    };
  },
  methods: {
    handleDrag(id) {
      const draggedRook = this.rooks.find((el) => el.id == id);
      this.draggedElement = draggedRook;
    },
    allowDrop(ev) {
      ev.preventDefault();
    },
    onDrop(event, row, col) {
      if (row && col) {
        //white rook
        if (
          this.draggedElement.id == 1 &&
          // movement rules
          (this.whiteRookPosition.row == row ||
            this.whiteRookPosition.col == col) &&
          //cell is not occupied
          this.checkFreePlace(row, col, 2)
        ) {
          this.whiteRookPosition = {
            col: col,
            row: row,
          };
        }
        //black rook
        if (
          this.draggedElement.id == 2 &&
          // movement rules
          (this.blackRookPosition.row == row ||
            this.blackRookPosition.col == col) &&
          //cell is not occupied
          this.checkFreePlace(row, col, 1)
        ) {
          this.blackRookPosition = {
            col: col,
            row: row,
          };
        }
      }
    },
    getCellClass(row, col) {
      const isWhite = (row + col) % 2 === 0;
      return isWhite ? "cell-white" : "cell-black";
    },
    checkFreePlace(row, col, rookId) {
      const otherRook =
        rookId == 2 ? this.blackRookPosition : this.whiteRookPosition;
      const newPosition = { col, row };
      return JSON.stringify(otherRook) !== JSON.stringify(newPosition);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
}
.chessboard {
  display: flex;
  flex-wrap: wrap;
  width: 640px;
  height: 640px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 80px;
}

.cell {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80px;
  height: 80px;
  font-size: 30px;
  font-weight: bold;
}
.cell-white {
  background-color: #f0d9b5;
}

.cell-black {
  background-color: #b58863;
}

.cell {
  background-color: #b58863;

  display: flex;
  align-items: center;
  justify-content: center;
  width: 80px;
  height: 80px;
  font-size: 30px;
  font-weight: bold;
}
</style>
