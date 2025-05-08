<script setup lang="ts">
import { ref } from "vue";
import api, { type GroupsBySensor } from "../api/api";
import CustomLoader from "./CustomLoader.vue";
import Summary from "./Summary.vue";
import CustomSelect from "./CustomSelect.vue";
import CustomList from "./CustomList.vue";
import SensorGroups from "./SensorGroups.vue";

const isLoading = ref(true);
const groupsBySensorData = ref<GroupsBySensor>({
  customer: "",
  groupsBySensor: {},
});

const selectedSensor = ref<string | undefined>(undefined);
const sensorOptions = ref<string[]>([]);

async function getData() {
  try {
    const data = await api.fetchGroupsBySensor();
    groupsBySensorData.value = data;
    sensorOptions.value = Object.keys(data.groupsBySensor);
  } catch (error) {
    console.error("Unable to get data:", error);
  } finally {
    isLoading.value = false;
  }
}

getData();
</script>

<template>
  <div class="container">
    <Transition name="fade" mode="out-in">
      <div class="spinner-container" v-if="isLoading">
        <CustomLoader />
      </div>
      <div v-else class="content">
        <Summary
          :customer="groupsBySensorData.customer ?? ''"
          :groupsBySensor="groupsBySensorData.groupsBySensor ?? {}"
        />
        <span class="sensor-select">
          <p>Sensor</p>
          <CustomSelect v-model="selectedSensor" :options="sensorOptions" />
          <p>is composed by:</p>
        </span>
        <Transition name="fade" mode="out-in">
          <div v-if="selectedSensor" class="sensor-info">
            <CustomList
              :listData="groupsBySensorData.groupsBySensor[selectedSensor]"
            />
            <SensorGroups
              :sensor="selectedSensor"
              :groups="groupsBySensorData.groupsBySensor"
            />
          </div>
        </Transition>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.spinner-container {
  display: flex;
  height: 100vh;
  align-items: center;
  justify-content: center;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  padding: 2.5rem;
}

.sensor-select {
  display: flex;
  align-items: center;
  justify-content: center;
  white-space: nowrap;
  gap: 1rem;
  width: 85%;
}

.sensor-info {
  width: 100%;
}
</style>
