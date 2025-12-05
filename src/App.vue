<script setup>
import { ref } from "vue";
import BaseTable from "./components/BaseTable.vue";

import CountryBadges from "./components/custom-cells/CountryBadges.vue";
import EmailCell from "./components/custom-cells/EmailCell.vue";
import ImageCell from "./components/custom-cells/ImageCell.vue";
import MarketCapCell from "./components/custom-cells/MarketCapCell.vue";
import PhoneFormatter from "./components/custom-cells/PhoneFormatter.vue";
import InputFilter from "./components/InputFilter.vue";
import rows from "./data.json";

const filteredRows = ref([...rows]);
const emailFilter = ref("");

// computed
const onFilter = ({ key, value }) => {
  if (key === "email") {
    filteredRows.value = rows.filter((row) =>
      String(row.email || "")
        .toLowerCase()
        .includes(value.toLowerCase())
    );
  }
};

const header = {
  firstName: "Имя",
  lastName: "Фамилия",
  email: "Почта",
  marketCap: "Капитализация",
  developedCountries: "Страны",
  phone: "Телефон",
  image: "Фото",
};

const resetFilters = () => {
  filteredRows.value = [...rows];
  emailFilter.value = "";
};
</script>

<template>
  <div class="p-5 flex justify-center">
    <button
      @click="resetFilters"
      class="bg-blue-500 text-white px-3 py-1 rounded hover:bg-blue-600"
    >
      Очистить фильтр
    </button>
  </div>
  <div class="p-4 flex justify-center">
    <BaseTable :rows="filteredRows" :header="header">
      <template #header-email="{ column }">
        <div class="flex items-center gap-2">
          <span>{{ header[column] }}</span>
          <InputFilter
            :column="column"
            placeholder="Фильтр"
            v-model="emailFilter"
            @filter="onFilter"
          />
        </div>
      </template>

      <template #email="{ value }">
        <EmailCell :value="value" />
      </template>
      <template #phone="{ value }">
        <PhoneFormatter :value="value" />
      </template>
      <template #developedCountries="{ value }">
        <CountryBadges :value="value" />
      </template>
      <template #marketCap="{ value }">
        <MarketCapCell :value="value" />
      </template>
      <template #image="{ value }">
        <ImageCell :value="value" />
      </template>
    </BaseTable>
  </div>
</template>
