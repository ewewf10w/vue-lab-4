<script setup>
defineProps({
  value: Array,
});
</script>

<template>
  <div class="flex flex-wrap gap-1">
    <span
      v-for="country in value"
      :key="country"
      class="bg-blue-100 text-blue-800 px-2 py-0.5 rounded"
    >
      {{ country }}
    </span>
  </div>
</template>
