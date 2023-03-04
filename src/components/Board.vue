<template class="drop-zone">
  <div v-for="row in 8" :key="row" class="row">
    <div v-for="col in 8" :key="col" :class="getCellClass(row, col)">
      <div class="cell"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Board",
  data() {
    return {};
  },
  emits: {},
  methods: {
    getCellClass(row, col) {
      const isWhite = (row + col) % 2 === 0;
      return isWhite ? "cell-white" : "cell-black";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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

.cell-white {
  background-color: #f0d9b5;
}

.cell-black {
  background-color: #b58863;
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
/* 800x600 */
@media (max-width: 600px) {
  .chessboard {
    width: 320px;
    height: 320px;
  }
  .cell {
    width: 40px;
    height: 40px;
  }
}
</style>
