<script setup lang="ts">
import MDraggableBoard from "./components/MDraggableBoard.vue";
import MDraggableItem from "./components/MDraggableItem.vue";
</script>

<template>
  <div class="main">
    <MDraggableBoard>
      <MDraggableItem>
        <h1>Card1</h1>
      </MDraggableItem>
    </MDraggableBoard>
    <MDraggableBoard>
      <MDraggableItem>
        <h1>Card2</h1>
      </MDraggableItem>
      <MDraggableItem>
        <h1>Card3</h1>
      </MDraggableItem>
    </MDraggableBoard>
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  transition: 0.4s;
}

.main {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  background-color: rgb(96, 96, 96);
}
</style>
