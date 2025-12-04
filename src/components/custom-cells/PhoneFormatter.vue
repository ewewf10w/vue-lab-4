<script setup>
defineProps({ value: String });

const formatPhone = (phone) => {
  let digits = phone.replace(/\D/g, "");
  if (digits.startsWith("8")) digits = "7" + digits.slice(1);
  return digits;
};
</script>

<template>
  <span>{{ formatPhone(value) }}</span>
</template>
