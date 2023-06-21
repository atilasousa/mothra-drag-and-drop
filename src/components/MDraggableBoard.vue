<template>
  <div
    @dragover.prevent="handleDragOver"
    @dragleave="handleDragLeave"
    @dragend="handleDragEnd"
    @drop.prevent="handleDrop"
    :class="draggableBoardClass()"
    :id="uniqueId"
  >
    <slot />
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import type { Ref } from "vue";
import { v4 as uuidv4 } from "uuid";
import bem from "bem-ts";

const draggableBoardClass = bem("mothra-draggable");

const uniqueId: Ref<string> = ref(uuidv4());

const handleDrop = (event: DragEvent) => {
  const card_id = event.dataTransfer!.getData("card_id");

  const card = document.getElementById(card_id);

  card!.style.display = "block";

  const board = event.target as any;

  board.appendChild(card);

  board.classList.remove(draggableBoardClass("hover"));
};

const handleDragOver = (event: DragEvent) => {
  const board = event.target as any;

  board.classList.add(draggableBoardClass("hover"));
};

const handleDragLeave = (event: DragEvent) => {
  const board = event.target as any;

  board.classList.remove(draggableBoardClass("hover"));
};

const handleDragEnd = (event: DragEvent) => {
  const board = event.target as any;

  board.classList.remove(draggableBoardClass("hover"));
};
</script>

<style lang="scss">
.mothra-draggable {
  background-color: black;
  width: 400px;
  height: auto;
  padding: 1rem 2rem;
  color: white;
  padding: 1rem;
  display: flex;
  justify-content: center;
  margin-right: 1rem;
  flex-direction: column;

  &__hover {
    border: 1px solid blue;
  }

  > *:last-child {
    margin-bottom: 0;
  }
}
</style>
