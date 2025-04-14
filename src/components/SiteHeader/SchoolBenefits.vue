<script setup lang="ts">
import { ButtonVariant } from "../../constants/button";
import AppButton from "../ui/AppButton.vue";

// Перечисление преимуществ школы
const schoolBenefits = [
  "private lessons",
  "group sessions",
  "gear rental",
  "balance training",
  "dune tours",
];
</script>

<template>
  <ul class="flex flex-wrap gap-[10px_18px] self-center">
    <li v-for="(benefit, index) in schoolBenefits" :key="index">
      <AppButton :variant="ButtonVariant.Header2">{{ $t(benefit) }}</AppButton>
    </li>
  </ul>
</template>
