<script setup>
import { computed, ref } from "vue";

const props = defineProps({
  rows: Array,
  header: Object,
});

const columns = computed(() => {
  const data = props.rows ?? [];
  if (Array.isArray(data) && data.length > 0) return Object.keys(data[0]);
  return Object.keys(props.header || {});
});
</script>

<template>
  <div class="w-full flex justify-center">
    <div class="bg-white shadow-md rounded-lg max-w-7xl w-full">
      <table class="w-full border-collapse">
        <thead>
          <tr class="bg-gray-100 border-b">
            <th
              v-for="key in columns"
              :key="key"
              class="px-4 py-2 text-left font-semibold text-gray-700 relative"
            >
              <div class="flex items-center justify-between">
                <slot :name="`header-${key}`" :column="key">
                  <span>{{ header[key] || key }}</span>
                </slot>
              </div>
            </th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="(row, rIndex) in rows"
            :key="rIndex"
            class="border-b hover:bg-gray-50 transition"
          >
            <td
              v-for="key in columns"
              :key="key"
              class="px-4 py-2 text-gray-800"
            >
              <slot :name="key" :value="row[key]">
                <span>{{ row[key] }}</span>
              </slot>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
