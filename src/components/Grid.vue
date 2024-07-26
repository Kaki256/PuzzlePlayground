<template>
    <div class="grid" @drop="handleDrop" @dragover="allowDrop">
      <div v-for="row in grid" :key="row[0].index" class="row">
        <div v-for="cell in row" :key="cell.index" class="cell">
          <slot :row="cell.rowIndex" :col="cell.colIndex"></slot>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, computed } from 'vue';
  
  const props = defineProps({
    rows: {
      type: Number,
      default: 10
    },
    cols: {
      type: Number,
      default: 10
    }
  });
  
  const grid = computed(() => {
    return Array.from({ length: props.rows }, (_, rowIndex) => {
      return Array.from({ length: props.cols }, (_, colIndex) => ({
        index: `${rowIndex}-${colIndex}`,
        rowIndex,
        colIndex,
      }));
    });
  });
  
  const allowDrop = (event) => {
    event.preventDefault();
  };
  
  const handleDrop = (event) => {
    // Drop handling logic
  };
  </script>
  
  <style scoped>
  .grid {
    display: grid;
    grid-template-rows: repeat(10, 50px);
    grid-template-columns: repeat(10, 50px);
    gap: 1px;
    margin: 20px auto;
    border: 1px solid #ddd;
    width: 510px; /* 50px x 10 cells + 9px gaps */
    height: 510px; /* 50px x 10 cells + 9px gaps */
  }
  .cell {
    width: 50px;
    height: 50px;
    background-color: #f0f0f0;
    border: 1px solid #ddd;
  }
  </style>
  