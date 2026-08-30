<template>
  <section>
    <div class="board">
      <cell v-for="(cell, index) in cells"
      :key="index"
      :bomb="cell"
      @click-cell="startGame(index)"
      />
    </div>
  </section>
</template>

<script setup>
import cell from '@/components/CellButton.vue'
import { ref } from 'vue';

const cells = ref(Array(81).fill(false));
const started = ref(false);

function startGame(index) {
  if (!started.value) {
    console.log("Iniciando run. Primeira célula: ", index);

    generateBombs(index);

    started.value = true;
  }
}

function generateBombs(firstCell) {
  let bombs = 0;

  while (bombs < 10) {
    const randomIndex = Math.floor(Math.random() * cells.value.length);

    if (randomIndex !== firstCell && !cells.value[randomIndex]) {
      cells.value[randomIndex] = true;
      bombs++;
    }
  }
}

</script>

<style scooped>
section {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.board {
  display: grid;
  grid-template-columns: repeat(9, 40px);
}
</style>
