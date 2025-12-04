<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  column: String,
  placeholder: String,
  modelValue: String,
});

const emit = defineEmits(["update:modelValue", "filter"]);

// локальное состояние input
const filterValue = ref(props.modelValue || "");

// синхронизация с родителем
watch(
  () => props.modelValue,
  (newVal) => {
    filterValue.value = newVal ?? "";
  }
);

// при вводе текста
const onInput = () => {
  emit("update:modelValue", filterValue.value);
  emit("filter", { key: props.column, value: filterValue.value });
};
</script>

<template>
  <input
    type="text"
    v-model="filterValue"
    @input="onInput"
    :placeholder="placeholder"
    class="border px-2 py-1 rounded w-full"
  />
</template>
