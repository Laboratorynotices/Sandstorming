<script setup lang="ts">
import { ButtonVariant } from "../constants/button";
import AppButton from "./ui/AppButton.vue";

// Список ключевых фраз для кнопок
const buttonPhrases = [
  "Catch the wind",
  "Dunes Calling",
  "Windy Freedom",
  "Sandsturm Hero",
];
</script>

<template>
  <div class="wrap-container site-about" id="about">
    <article class="flex flex-col md:flex-row w-full">
      <!-- Левая колонка -->
      <div class="w-full md:w-1/2 flex flex-col justify-between md:pr-2.5">
        <header class="xl:w-2/3">
          <h1 class="font-bold">About Us</h1>
          <h2>
            {{ $t("Sandstorming School. Ghardaïa.") }}
          </h2>
        </header>

        <ul class="flex flex-wrap gap-[10px_18px] xl:w-2/3">
          <li v-for="(phrase, index) in buttonPhrases" :key="index">
            <AppButton :variant="ButtonVariant.Header2">{{
              $t(phrase)
            }}</AppButton>
          </li>
        </ul>

        <div class="my-[1em] md:mb-0 xl:w-2/3">
          <p class="text-base mb-[1em]">
            {{ $t("About us. Paragraph 1.") }}
          </p>
          <p class="text-base">
            {{ $t("About us. Paragraph 2.") }}
          </p>
        </div>
      </div>
      <!-- Правая колонка -->
      <div class="w-full md:w-1/2 relative">
        <img
          src="/src/assets/images/about-us.png"
          alt="About Us"
          class="max-w-[100%]"
        />
        <AppButton
          :variant="ButtonVariant.Header2"
          href="#activities"
          class="activities_button absolute uppercase"
          >{{ $t("activities") }}</AppButton
        >
      </div>
    </article>
  </div>
</template>

<style lang="css" scoped>
.site-about {
  margin-bottom: clamp(50px, 11vw, 150px);
}

.activities_button {
  right: clamp(5px, 3.5vw, 50px);
  bottom: clamp(5px, 3.5vw, 50px);
}
</style>
