<script setup>
defineProps({
  value: String,
});
</script>

<template>
  <a :href="`mailto:${value}`" class="text-blue-500 underline">
    {{ value }}
  </a>
</template>
