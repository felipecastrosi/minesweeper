<template>
  <div class="cell"
  :class="{
    bomb: bomb && clicked,
    safe: !bomb && clicked,
    flagged: !clicked && flag
  }"
  @mousedown="mouseDown"
  @contextmenu.prevent
  >
</div>
</template>

<script setup>
import { ref } from 'vue';
const props = defineProps({
  bomb: Boolean
});
const emit = defineEmits(['click-cell']);
console.log(props);

function mouseDown(event) {
  if (event.button === 0) {
    leftClick();
  }

  if (event.button === 2) {
    rightClick();
  }
}

function leftClick() {
  if (!flag.value && !clicked.value) {
    clicked.value = true;
    emit('click-cell');
  }
}
function rightClick() {
  if (!clicked.value) {
    flag.value = !flag.value;
  }
}

const clicked = ref(false);
const flag = ref(false);
</script>

<style scooped>
.cell {
  width: 40px;
  height: 40px;
  background-color: black;
  border: 1px solid grey;
  box-sizing: border-box;
}

.cell.bomb {
  background-color: red;
}

.cell.safe {
  background-color: green;
}

.cell.flagged {
  background-color: white;
}
</style>
