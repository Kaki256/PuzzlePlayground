<template>
  <div id="app">
    <div>
      n = <input type="number" v-model.number="gridSize" min="1" max="20" />
    </div>
    <Grid :rows="gridSize" :cols="gridSize">
      <template #default="{ row, col }">
        <div class="grid-cell">
          <div v-if="grid[row][col]" :style="{ backgroundColor: grid[row][col] }" class="filled-cell"></div>
        </div>
      </template>
    </Grid>
    <div class="polyomino-container">
      <Polyomino :shape="[[1, 1], [1, 1]]" color="#e74c3c" />
      <Polyomino :shape="[[1, 1, 1], [0, 1, 0]]" color="#8e44ad" />
    </div>
    <button @click="addPiece">ピース追加</button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import Grid from './components/Grid.vue';
import Polyomino from './components/Polyomino.vue';

const gridSize = ref(10);
const grid = ref(Array(gridSize.value).fill().map(() => Array(gridSize.value).fill(null)));

watch(gridSize, (newSize) => {
  grid.value = Array(newSize).fill().map(() => Array(newSize).fill(null));
});

const addPiece = () => {
  // ピース追加のロジック
};
</script>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
.polyomino-container {
  display: flex;
  gap: 10px;
}
.filled-cell {
  width: 50px;
  height: 50px;
}
.grid-cell {
  position: relative;
}
</style>
