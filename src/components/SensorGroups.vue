<script setup lang="ts">
import { computed } from "vue";
import { type GroupsBySensor } from "../api/api";

type SensorGroupsProps = {
  sensor: string;
  groups: GroupsBySensor["groupsBySensor"];
};

const { sensor, groups } = defineProps<SensorGroupsProps>();

const sensorPrefix = computed(() => {
  return sensor?.split("_")[0] ?? "";
});
const groupsQuantity = computed(() => {
  return groups[sensor].length ?? 0;
});
</script>

<template>
  <div class="sensor-groups">
    <p>
      Sensor prefixed with <b>{{ sensorPrefix }}</b> contains a total of
      <b>{{ groupsQuantity }}</b> {{ groupsQuantity > 1 ? "groups" : "group" }}
    </p>
  </div>
</template>

<style scoped>
.sensor-groups {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  margin-top: 1.5rem;
  padding: 0.5rem 0;
  border-top: 2px solid #002cf6;
}
</style>
