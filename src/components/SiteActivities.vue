<script setup lang="ts">
import { ButtonVariant } from "../constants/button";
import AppButton from "./ui/AppButton.vue";
import { useI18n } from "vue-i18n";

// Импортируем useI18n из vue-i18n для работы с локализацией
// Сможем использовать его для получения текущего языка и перевода текста
const { locale } = useI18n();

// Перечисление преимуществ школы
const schoolBenefits = [
  "private lessons2",
  "group sessions2",
  "gear rental2",
  "balance training2",
  "dune tours2",
];
</script>

<template>
  <article class="wrap-container activities">
    <h1 id="activities">{{ $t("activities") }}</h1>
    <div class="md:flex">
      <!-- Левый столбик -->
      <div class="w-full md:w-1/2">
        <h2 class="md:w-2/3">
          {{
            $t(
              "No doldrums or stagnation - sand dunes in a storm is your best adventure.",
            )
          }}
        </h2>
      </div>
      <!-- Правый столбик -->
      <div class="flex flex-col justify-between gap-[2em] w-full md:w-1/2">
        <div>
          <p>{{ $t("Activities. Paragraph 1.") }}</p>
          <p>{{ $t("Activities. Paragraph 2.") }}</p>
        </div>
        <AppButton class="w-fit" href="#" :variant="ButtonVariant.Event1">{{
          $t("book now")
        }}</AppButton>
      </div>
    </div>

    <ul class="flex flex-wrap self-center benefits-list">
      <li
        v-for="(benefit, index) in schoolBenefits"
        :key="index"
        class="bg-overlay text-text border-text border rounded-full aspect-square w-full sm:w-1/2 md:w-1/5 flex justify-center items-center text-center"
      >
        <span :lang="locale" class="max-w-2/3 hyphens-auto">
          {{ $t(benefit) }}
        </span>
      </li>
    </ul>
  </article>
  <div
    class="bg-[url('./assets/images/activities.png')] bg-no-repeat bg-cover bg-[bottom_center] h-[20vw] mb-[5vw]"
  ></div>
</template>

<style lang="css" scoped>
.activities {
  margin-bottom: clamp(50px, 11vw, 150px);
}
.benefits-list {
  margin-top: clamp(30px, 7vw, 100px);
}
</style>
