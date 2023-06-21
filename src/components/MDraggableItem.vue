<template>
  <div
    :id="uniqueId"
    :class="draggableItemClass()"
    :draggable="draggable"
    @dragstart="handleDragStart"
    @dragend="handleDragEnd"
    @dragover.stop
  >
    <slot />
  </div>
</template>
<script lang="ts" setup>
import { ref } from "vue";
import type { Ref } from "vue";
import { v4 as uuidv4 } from "uuid";
import bem from "bem-ts";

const uniqueId: Ref<string> = ref(uuidv4());

const draggableItemClass = bem("mothra-draggable-item");

const handleDragEnd = (event: DragEvent) => {
  const target = event.target as HTMLElement;
  const draggableBoard = target.parentElement!.closest(".mothra-draggable");

  if (draggableBoard) {
    target.style.display = "block";
  } else {
    target.style.display = "none";
  }

  target.classList.remove(draggableItemClass("hover"));
};

const handleDragStart = (event: DragEvent) => {
  const target = event.target as HTMLElement;

  target.classList.add(draggableItemClass("hover"));
  event.dataTransfer!.setData("card_id", target.id);

  setTimeout(() => {
    target.classList.add("hover");
  }, 0);
};

withDefaults(
  defineProps<{
    draggable?: boolean;
  }>(),
  {
    draggable: true,
  }
);
</script>
<style lang="scss">
.mothra-draggable-item {
  background-color: white;
  color: black;
  margin-bottom: 1rem;

  &__hover {
    background-color: rgb(206, 206, 206);
  }
}
</style>
