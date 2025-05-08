<script setup lang="ts">
import { ref } from "vue";
import ComponentsPreview from "./components/ComponentsPreview.vue";
import SensorExplorer from "./components/SensorExplorer.vue";

const showPreview = ref(true);
</script>

<template>
  <ComponentsPreview v-if="showPreview" />
  <SensorExplorer v-else />
</template>

<style scoped></style>
