<template>
  <div class="board" @dragover="allowDrop" @drop="onDrop">
    <div v-for="row in 8" :key="row" class="row">
      <div v-for="col in 8" :key="col">
        <Cell
          @drop="onDrop($event, row, col)"
          @onDraggedElement="handleDrag"
          :computed-class="getCellClass(row, col)"
          :row="row"
          :col="col"
          :has-element="hasElement(row, col)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Cell from "./components/Cell.vue";
export default {
  name: "App",
  components: {
    Cell,
  },
  data() {
    return {
      elements: [
        { id: "1", color: "white", col: 1, row: 1, type: "rook" },
        { id: "2", color: "black", col: 1, row: 8, type: "rook" },
      ],
      draggedElement: {},
    };
  },
  methods: {
    handleDrag(id) {
      const draggedElement = this.elements.find((el) => el.id == id);
      this.draggedElement = draggedElement;
    },
    allowDrop(ev) {
      ev.preventDefault();
    },
    hasElement(row, col) {
      const targetElement = this.elements.find(
        (el) => el.row == row && el.col == col
      );
      if (targetElement) {
        return targetElement;
      } else return false;
    },
    onDrop(event, row, col) {
      if (row && col) {
        const targetElement = this.elements.find(
          (el) => el.id === this.draggedElement.id
        );
        if (
          this.checkFreePlace(row, col) &&
          this.checkMovementRules(targetElement, row, col)
        ) {
          targetElement.col = col;
          targetElement.row = row;
        }
      }
    },
    getCellClass(row, col) {
      const isWhite = (row + col) % 2 === 0;
      return isWhite ? "cell-white" : "cell-black";
    },

    checkFreePlace(row, col) {
      return !this.elements.find((el) => el.row == row && el.col == col);
    },
    checkMovementRules(element, row, col) {
      switch (element.type) {
        case "rook":
          return element.col == col || element.row == row;

        // в остальные case можно положить другие типы шахматных фигур, в проверку - соответствующие правила

        default:
          break;
      }
    },
  },
};
</script>

<style>
.board {
  display: flex;
  flex-wrap: wrap;
  margin: 6rem auto;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

/* .cell {
  display: flex;
  align-items: center;
  justify-content: center;
} */
.cell-white {
  background-color: #f0d9b5;
}

.cell-black {
  background-color: #b58863;
}

/* 390х844 */
@media (min-width: 390px) {
  .board {
    width: 320px;
    height: 320px;
  }
}
/* 800х600 */
@media (min-width: 800px) {
  .board {
    width: 640px;
    height: 640px;
  }
}
/* 1920х1080 */
@media (min-width: 1920px) {
  .board {
    width: 800px;
    height: 800px;
  }
}
</style>
