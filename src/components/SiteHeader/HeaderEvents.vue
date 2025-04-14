<script setup lang="ts">
import { ButtonVariant } from "../../constants/button";
import AppButton from "../ui/AppButton.vue";

// Список событий
const events = [
  {
    imageName: "red-dune-rumble.png",
    title: "Red Dune Rumble",
    date: "15–17 November 2025",
    location: "Dubai Dunes, UAE",
  },
  {
    imageName: "sand-surge-showdown.png",
    title: "Sand Surge Showdown",
    date: "23–25 May 2025",
    location: "White Sands, New Mexico, USA",
  },
  {
    imageName: "sandstorm-showdown.png",
    title: "Sandstorm Showdown",
    date: "13–15 July 2025",
    location: "Great Sand Dunes, Colorado, USA",
  },
];

// Выбираем случайное событие из списка
const randomEvent = events[Math.floor(Math.random() * events.length)];
</script>

<template>
  <div
    class="event_block flex flex-col justify-between mx-auto w-fit md:mx-0 md:justify-self-end"
  >
    <div
      class="event_card bg-overlay mx-auto p-2.5 w-max rounded-sm md:pt-10 md:mr-0"
    >
      <h1 class="font-extrabold">{{ randomEvent.title }}</h1>
      <h2 class="font-extrabold">{{ randomEvent.date }}</h2>
      <h3 class="font-extrabold">{{ randomEvent.location }}</h3>
      <a class="font-extrabold uppercase underline underline-offset-2" href="#"
        >more info</a
      >
      <img
        :src="`/src/assets/images/events/${randomEvent.imageName}`"
        :alt="randomEvent.title"
        :title="randomEvent.title"
        class="max-h-[50vh] max-w-[85vw]"
      />
    </div>
    <div
      class="button_row flex flex-wrap gap-[1em] justify-between my-2.5 md:mb-0"
    >
      <AppButton href="#" :variant="ButtonVariant.Event1">{{
        $t("book now")
      }}</AppButton>
      <AppButton href="#" :variant="ButtonVariant.Event2">{{
        $t("activities")
      }}</AppButton>
    </div>
  </div>
</template>

<style lang="css" scoped>
h1,
h2,
h3 {
  font-size: clamp(20px, 2.5vw, 32px);
}
a {
  font-size: clamp(12px, 1.5vw, 20px);
}
</style>
