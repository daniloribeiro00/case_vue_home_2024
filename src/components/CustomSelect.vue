<script setup lang="ts">
import { type PropType, ref } from "vue";

defineProps({
  modelValue: {
    type: String as PropType<string>,
    default: undefined,
  },
  options: { type: Array as PropType<string[]>, required: true },
  placeholder: { type: String as PropType<string>, default: "Select a value" },
});

const emit = defineEmits<{
  "update:modelValue": [option: string];
}>();

const isDropdownOpen = ref(false);

function onOptionClick(option: string) {
  emit("update:modelValue", option);
}
</script>

<template>
  <div class="select-wrapper" @click="isDropdownOpen = !isDropdownOpen">
    <div :class="{ select: true, open: isDropdownOpen }">
      <div :class="{ select__trigger: true, placeholder: !modelValue }">
        <span>{{ modelValue || placeholder }}</span>
        <div class="arrow"></div>
      </div>
      <div class="custom-options">
        <span
          v-for="option in options"
          :key="option"
          :class="{ 'custom-option': true, selected: option === modelValue }"
          :data-value="option"
          @click="() => onOptionClick(option)"
        >
          {{ option }}
        </span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.select-wrapper {
  position: relative;
  user-select: none;
  width: 100%;
}

.select {
  position: relative;
  display: flex;
  flex-direction: column;
}

.select__trigger {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 10px;
  font-size: 14px;
  font-weight: 300;
  color: #aeaeba;
  line-height: 32px;
  background: #303438;
  cursor: pointer;
  border-width: 1px 1px 1px 1px;
  border-style: solid;
  border-color: #696c6f;
  border-radius: 8px;
}

.select__trigger.placeholder {
  color: #636363;
}

.custom-options {
  position: absolute;
  display: block;
  top: 100%;
  left: 0;
  right: 0;
  border: 1px solid #696c6f;
  border-radius: 4px;
  border-top: 0;
  background: #303438;
  transition: all 0.5s;
  opacity: 0;
  visibility: hidden;
  pointer-events: none;
  z-index: 2;
}

.select.open .custom-options {
  opacity: 1;
  visibility: visible;
  pointer-events: all;
}

.custom-option {
  position: relative;
  display: block;
  padding: 0 10px;
  font-size: 14px;
  font-weight: 300;
  color: #aeaeba;
  line-height: 32px;
  cursor: pointer;
  transition: all 0.5s;
}

.custom-option:hover {
  cursor: pointer;
  background-color: #232629;
  border-radius: 4px;
}
.custom-option.selected {
  color: #ffcc0d;
}

.arrow {
  position: relative;
  height: 15px;
  width: 15px;
}
.arrow::before,
.arrow::after {
  content: "";
  position: absolute;
  bottom: 0px;
  width: 0.15rem;
  height: 100%;
  transition: all 0.5s;
}

.arrow::before {
  left: -5px;
  transform: rotate(45deg);
  background-color: #696c6f;
}

.arrow::after {
  left: 5px;
  transform: rotate(-45deg);
  background-color: #696c6f;
}

.open .arrow::before {
  left: -5px;
  transform: rotate(-45deg);
}

.open .arrow::after {
  left: 5px;
  transform: rotate(45deg);
}
</style>
