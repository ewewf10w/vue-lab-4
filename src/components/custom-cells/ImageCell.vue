<template>
  <img
    v-if="value"
    :src="value"
    alt="img"
    class="w-10 h-10 rounded-full object-cover"
  />
</template>

<script setup>
defineProps({
  value: String,
});
</script>
