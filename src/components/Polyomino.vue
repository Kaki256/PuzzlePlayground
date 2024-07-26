<template>
    <div class="polyomino" :style="{ width: width + 'px', height: height + 'px' }">
      <div v-for="(row, rowIndex) in shape" :key="rowIndex" class="row">
        <div v-for="(cell, colIndex) in row" :key="colIndex" class="cell"
             :style="cell === 1 ? { backgroundColor: color } : {}">
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, computed } from 'vue';
  
  const props = defineProps({
    shape: {
      type: Array,
      required: true
    },
    color: {
      type: String,
      required: true
    }
  });
  
  const width = computed(() => props.shape[0].length * 50);
  const height = computed(() => props.shape.length * 50);
  </script>
  
  <style scoped>
  .polyomino {
    display: grid;
    gap: 1px;
  }
  
  .row {
    display: flex;
  }
  
  .cell {
    width: 50px;
    height: 50px;
    border: 1px solid #ddd;
  }
  </style>
  