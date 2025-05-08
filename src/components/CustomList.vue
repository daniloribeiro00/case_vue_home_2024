<script setup lang="ts">
import type { PropType } from "vue";

defineProps({
  listData: {
    type: Array as PropType<string[] | undefined>,
    default: undefined,
  },
});
</script>

<template>
  <div v-if="listData" class="list">
    <span v-for="element in listData" :key="element" class="element">
      {{ element }}
    </span>
  </div>
</template>

<style scoped>
.list {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 40px;
  width: 100%;
  border-width: 3px 0;
  border-style: solid;
  border-color: #41474d;
  border-radius: 8px;
}

.element {
  font-size: 12px;
  margin: 0 4px;
  padding: 8px;
  background-color: #41474d;
  border-radius: 8px;
}
</style>
