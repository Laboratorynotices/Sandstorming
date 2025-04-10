<script setup lang="ts">
// Определяем события
const emit = defineEmits(["linkClicked"]);

// Массив пунктов меню
const navItems = [
  { id: 1, name: "home", path: "/" },
  { id: 2, name: "who we are", path: "/about" },
  { id: 3, name: "activities", path: "/activities" },
  { id: 4, name: "review", path: "/review" },
];

// Функция для обработки клика по ссылке
const handleLinkClick = () => {
  emit("linkClicked");
};
</script>

<template>
  <ul class="md:flex md:space-x-6">
    <li v-for="item in navItems" :key="item.id" class="mb-4 md:mb-0">
      <a
        :href="item.path"
        @click="handleLinkClick"
        class="text-primary hover:text-primary-light transition-colors duration-300 block py-2 md:py-0"
      >
        {{ $t(item.name) }}
      </a>
    </li>
  </ul>
</template>
