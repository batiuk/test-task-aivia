<template>
  <div class="game-view">
    <v-row>
      <v-col cols="6">
        <v-text-field
          @change="generateSquares"
          label="Size X"
          v-model="sizeX"
          type="number"/>
      </v-col>
      <v-col cols="6">
        <v-text-field
          @change="generateSquares"
          label="Size Y"
          v-model="sizeY"/>
      </v-col>
    </v-row>

    <div>
      <div v-for="i in sizeY" :key="`row-${i}`" class="row">
        <div v-for="j in sizeX" :key="`column-${j}`"
             class="square"
             :class="{ 'square--blue': squares[i-1][j-1], 'square--white': !squares[i-1][j-1] }"
             @mouseenter="toggleSquare(i-1, j-1)">
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue';

const sizeX = ref(100);
const sizeY = ref(100);
const squares = ref([]);

function toggleSquare(x, y) {
  squares.value[x][y] = !squares.value[x][y];
}
function generateSquares() {
  squares.value = [];
  for (let i = 0; i < sizeY.value; i++) {
    squares.value[i] = new Array(sizeX.value).fill(false);
  }
}

generateSquares();
</script>

<style>
.row {
  display: flex;
  flex-wrap: nowrap;
}

.square {
  width: 36px !important;
  height: 36px !important;
  border: 1px solid grey;
  background-color: white;
}

.square--blue {
  background-color: blue;
}

.square--white {
  background-color: white;
}
</style>
