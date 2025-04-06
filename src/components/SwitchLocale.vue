<script setup lang="ts">
import { useI18n } from "vue-i18n";

import { setLocale } from "/src/i18n";
const { locale } = useI18n();

async function switchLocale() {
  const newLocale = locale.value === "de" ? "ru" : "de";
  await setLocale(newLocale);
}
</script>

<template>
  <div>
    <p>{{ $t("hello") }}</p>
    <button @click="switchLocale">Switch language</button>
  </div>
</template>
