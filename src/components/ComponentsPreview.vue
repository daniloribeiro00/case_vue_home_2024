<script setup lang="ts">
import { ref } from "vue";

import CustomLoader from "./CustomLoader.vue";
import CustomList from "./CustomList.vue";
import CustomSelect from "./CustomSelect.vue";
import Summary from "./Summary.vue";

const groupsBySensor = {
  sensor1Example: ["Group1Example", "Group2Example", "Group3Example"],
  sensor2Example: ["Group1Example", "Group2Example"],
};

const selectValue = ref(undefined);
</script>

<template>
  <div class="componentsPreview">
    <span class="label">Summary:</span>
    <Summary customer="Example" :groupsBySensor="groupsBySensor" />

    <span class="label">CustomLoader:</span>
    <CustomLoader />

    <span class="label">CustomSelect:</span>
    <CustomSelect v-model="selectValue" :options="['Option 1', 'Option 2']" />

    <span class="label">CustomList:</span>
    <CustomList :listData="['Entry1', 'Entry2']" />
  </div>
</template>

<style scoped>
.componentsPreview {
  display: grid;
  grid-template-columns: 1fr 4fr;
  gap: 16px;
  align-items: center;
  justify-items: start;
  background-color: black;
  padding: 16px;
}

.label {
  justify-self: start;
  font-size: 16px;
}
</style>
