<!--  -->

<template>
  <div class="cell" :class="computedClass">
    <div draggable="true">
      <Rook
        @onDragged="onDragged"
        class="rook"
        v-if="hasWhiteRook"
        :color="`white`"
        :id="1"
      />
      <Rook
        @onDragged="onDragged"
        class="rook"
        v-if="hasBlackRook"
        :color="`black`"
        :id="2"
      />
    </div>
  </div>
</template>

<script>
import Rook from "./Rook.vue";

export default {
  name: "Cell",
  data() {
    return {};
  },
  components: {
    Rook,
  },
  props: {
    row: {
      required: true,
      type: Number,
    },
    col: {
      required: true,
      type: Number,
    },
    computedClass: {
      required: true,
      type: String,
    },
    whiteRookPosition: {},
    blackRookPosition: {},
  },
  computed: {
    hasWhiteRook() {
      if (
        this.whiteRookPosition.col === this.col &&
        this.whiteRookPosition.row === this.row
      ) {
        return true;
      }
      return false;
    },
    hasBlackRook() {
      if (
        this.blackRookPosition.col === this.col &&
        this.blackRookPosition.row === this.row
      ) {
        return true;
      }
      return false;
    },
  },
  methods: {
    onDragged(id) {
      this.$emit("onDraggedElement", id);
    },
  },
};
</script>

<style scoped>
.cell-white {
  background-color: #f0d9b5;
}
.rook {
  transform: translate(0, 0);
}

.cell {
  width: 80px;
  height: 80px;
}
.cell-black {
  background-color: #b58863;
}
</style>
