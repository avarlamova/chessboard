<template>
  <div class="rook" draggable="true" @dragstart="onDragStart(id)">
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
      type: String,
    },
  },

  methods: {
    onDragStart(id) {
      this.$emit("onDragged", id);
    },
  },
};
</script>

<style scoped>
.rook {
  transform: translate(0, 0);
}

svg {
  color: v-bind(color);
}

/* 390х844 */
@media (min-width: 390px) {
  svg {
    width: 40px;
    height: 40px;
  }
}
/* 800х600 */
@media (min-width: 800px) {
  svg {
    width: 80px;
    height: 80px;
  }
}
/* 1920х1080 */
@media (min-width: 1920px) {
  svg {
    width: 100px;
    height: 100px;
  }
}
</style>
