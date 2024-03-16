<template>
  <div>
    <div
      v-for="(block, index) in blocks"
      :key="index"
      class="draggable"
      :style="{ left: block.posX + 'px', top: block.posY + 'px' }"
      @mousedown="startDragging(index, $event)"
    >
      <div class="drag-handle">Drag me</div>
      <div class="content">Content inside draggable</div>
    </div>
    <button @click="addBlock">Add Block</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blocks: [],
    };
  },
  methods: {
    startDragging(index, event) {
      this.blocks[index].dragging = true;
      this.blocks[index].mouseX = event.clientX;
      this.blocks[index].mouseY = event.clientY;
      document.addEventListener('mousemove', this.drag(index));
      document.addEventListener('mouseup', this.stopDragging(index));
    },
    stopDragging(index) {
      return () => {
        this.blocks[index].dragging = false;
        document.removeEventListener('mousemove', this.drag(index));
        document.removeEventListener('mouseup', this.stopDragging(index));
      };
    },
    drag(index) {
      return (event) => {
        if (this.blocks[index].dragging) {
          const deltaX = event.clientX - this.blocks[index].mouseX;
          const deltaY = event.clientY - this.blocks[index].mouseY;
          this.blocks[index].posX += deltaX;
          this.blocks[index].posY += deltaY;
          this.blocks[index].mouseX = event.clientX;
          this.blocks[index].mouseY = event.clientY;
        }
      };
    },
    addBlock() {
      this.blocks.push({ dragging: false, posX: 0, posY: 0, mouseX: 0, mouseY: 0 });
    },
  },
};
</script>

<style scoped>
.draggable {
  position: absolute;
  width: 200px;
  height: 200px;
  background-color: #1220e6;
  border: 1px solid #ccc;
  cursor: move;
}

.drag-handle {
  padding: 8px;
  background-color: #ccc;
}

.content {
  padding: 8px;
}
</style>
