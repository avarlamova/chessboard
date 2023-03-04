<template>
  <div class="cell" :class="computedClass">
    <div draggable="true">
      <component
        :is="elementType"
        :color="hasElement.color"
        :id="hasElement.id"
        @onDragged="onDragged"
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
    hasElement: {
      required: true,
    },
  },
  computed: {
    elementType() {
      if (this.hasElement) {
        const { type } = this.hasElement;
        //предположим, что типов фигур будет много, поэтому использован switch
        switch (type) {
          case "rook":
            return Rook;

          default:
            break;
        }
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

.cell {
  width: 80px;
  height: 80px;
}
.cell-black {
  background-color: #b58863;
}
</style>
