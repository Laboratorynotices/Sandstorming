<script setup lang="ts">
// Список фраз
const phrases = [
  "FEAR IS JUST THE WIND BEFORE YOU FLY.",
  "THE DUNE YOU DREAD TODAY WILL CARRY YOU TOMORROW.",
  "WHEN YOU RIDE WITH THE STORM, LIMITS FADE AWAY.",
  "EVERY GRAIN OF SAND KNOWS YOUR POTENTIAL.",
  "SILENCE THE DOUBT — LET THE DESERT SPEAK.",
];

// Выбираем случайную фразу из списка
const randomPhrase = phrases[Math.floor(Math.random() * phrases.length)];
</script>

<template>
  <div class="wrap-container site-phrase">
    <blockquote class="font-extrabold w-2/3">{{ $t(randomPhrase) }}</blockquote>
  </div>
</template>

<style lang="css" scoped>
blockquote {
  font-size: clamp(20px, 4.5vw, 64px);
  margin: clamp(60px, 9vw, 120px) 0;
}
</style>
