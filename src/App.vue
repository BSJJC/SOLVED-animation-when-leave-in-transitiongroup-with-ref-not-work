<template>
  <TransitionGroup name="container" tag="ul" class="container">
    <div v-for="(_, index) in counts" :key="_">
      {{ index }}

      <!-- animation when leave doesn't work -->
      <!-- <input ref="inputRef" /> -->

      <!-- animation works with shallowRef -->
      <input ref="inputShallowRef" />

      <!-- animation when leave works -->
      <!-- <input /> -->

      <button @click="remove(index)">delete</button>
    </div>

    <button @click="add">add input</button>
  </TransitionGroup>
</template>

<script setup lang="ts">
import { ref, shallowRef } from "vue";

const counts = ref([1, 2, 3, 4, 5]);
const inputRef = ref();
const inputShallowRef = shallowRef();

const add = () => {
  counts.value.push(counts.value[counts.value.length - 1] + 1);
};

const remove = (index) => {
  counts.value.splice(index, 1);
};
</script>

<style>
.container {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 1rem;
  row-gap: 2rem;
  background: #add8e620;
}

.container-move,
.container-enter-active,
.container-leave-active {
  transition: all 0.3s ease-in-out;
}

.container-enter-from,
.container-leave-to {
  opacity: 0;
  transform: translateX(50px);
}

.container-leave-active {
  position: absolute;
}
</style>
