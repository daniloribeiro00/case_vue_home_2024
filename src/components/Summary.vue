<script setup lang="ts">
import { PropType, computed } from "vue";

const props = defineProps({
  customer: {
    type: String as PropType<string>,
    default: undefined,
  },
  groupsBySensor: {
    type: Object as PropType<Record<string, string[]>>,
    default: undefined,
  },
});

const numOfSensors = computed(() =>
  props.groupsBySensor ? Object.keys(props.groupsBySensor).length : undefined
);

const numOfGroups = computed(() =>
  props.groupsBySensor
    ? new Set(
        Object.values(props.groupsBySensor).reduce(
          (res, groups) => [...res, ...groups],
          []
        )
      ).size
    : undefined
);
</script>

<template>
  <div class="summary">
    Customer
    <strong>{{ customer || "?" }}</strong>
    contains
    <strong>{{ numOfSensors || "?" }}</strong>
    sensors used in
    <strong>{{ numOfGroups || "?" }}</strong>
    groups.
  </div>
</template>

<style scoped>
.summary {
  text-align: center;
  padding: 16px;
  color: white;
  background-color: #41474d;
  border-radius: 8px;
}
</style>
