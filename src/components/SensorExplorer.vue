<script setup lang="ts">
import { ref } from "vue";
import api, { type GroupsBySensor } from "../api/api";
import CustomLoader from "./CustomLoader.vue";
import Summary from "./Summary.vue";
import CustomSelect from "./CustomSelect.vue";
import CustomList from "./CustomList.vue";

const isLoading = ref(true);
const groupsBySensor = ref<GroupsBySensor>({
  customer: "",
  groupsBySensor: {},
});

const selectSensor = ref<string | undefined>(undefined);
const sensorOptions = ref<string[]>([]);

async function getData() {
  try {
    const data = await api.fetchGroupsBySensor();
    groupsBySensor.value = data;
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
          :customer="groupsBySensor.customer ?? ''"
          :groupsBySensor="groupsBySensor.groupsBySensor ?? {}"
        />
        <div class="sensor">
          <p>Sensor</p>
          <CustomSelect v-model="selectSensor" :options="sensorOptions" />
          <p>is composed by:</p>
        </div>
        <Transition name="fade" mode="out-in">
          <CustomList
            v-if="selectSensor"
            :listData="groupsBySensor.groupsBySensor[selectSensor]"
          />
        </Transition>
      </div>
    </Transition>
  </div>

  <!-- TODO: Uncomment once part 1 is complete -->
  <!-- <SensorGroups /> -->
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

.sensor {
  display: flex;
  align-items: center;
  justify-content: center;
  white-space: nowrap;
  gap: 1rem;
  width: 85%;
}
</style>
