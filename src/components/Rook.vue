<template>
  <div draggable="true" @dragstart="onDragStart(id)">
    <CastleImage />
  </div>
</template>

<script>
import CastleImage from "./CastleImage";

export default {
  name: "Rook",
  data() {
    return {};
  },
  components: {
    CastleImage,
  },
  props: {
    color: {
      required: true,
      type: String,
    },
    id: {
      required: true,
      type: Number,
    },
  },

  methods: {
    onDragStart(id) {
      this.$emit("onDragged", id);
    },
    onMouseDown(event) {
      event.preventDefault();
      this.isDragging = true;
      this.originalX = event.clientX;
      this.originalY = event.clientY;
      document.addEventListener("mousemove", this.onMouseMove);
      document.addEventListener("mouseup", this.onMouseUp);
    },
    onMouseMove(event) {
      if (this.isDragging) {
        this.currentX = event.clientX - this.originalX;
        this.currentY = event.clientY - this.originalY;
        this.xOffset = this.position.left + this.currentX;
        this.yOffset = this.position.top + this.currentY;
        this.$refs.rook.style.top = `${this.yOffset}px`;
        this.$refs.rook.style.left = `${this.xOffset}px`;
      }
    },
    onMouseUp() {
      this.isDragging = false;
      document.removeEventListener("mousemove", this.onMouseMove);
      document.removeEventListener("mouseup", this.onMouseUp);
      const newPosition = {
        top: `${this.yOffset}px`,
        left: `${this.xOffset}px`,
      };
      this.$emit("onMove", newPosition);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* div {
  background-color: v-bind(color);
} */

svg {
  color: v-bind(color);
}
</style>
