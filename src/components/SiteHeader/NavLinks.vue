<script setup lang="ts">
// Определяем пропсы для компонента
defineProps({
  hideMenu: {
    type: Boolean,
    required: true,
  },
  isMobile: {
    type: Boolean,
    required: true,
  },
  isMenuOpen: {
    type: Boolean,
    required: true,
  },
});
// Массив пунктов меню
const navItems = [
  { id: 1, name: "home", path: "#" },
  { id: 2, name: "who we are", path: "#about" },
  { id: 3, name: "activities", path: "#activities" },
  { id: 4, name: "review", path: "#review" },
];
</script>

<template>
  <!-- Навигационные ссылки (один компонент для обоих режимов) -->
  <ul
    id="nav-container"
    class="md:flex md:space-x-6"
    :class="[
      // На пару секунд скрываем меню при переходе с десктопа на мобильный
      hideMenu ? 'hidden' : '',
      // Условные стили для мобильной версии
      isMobile
        ? 'fixed left-0 right-0 top-0 bg-background z-10 pt-16 p-4 transition-all duration-300 ease-in-out'
        : 'relative',
      // Анимация появления/скрытия только для мобильной версии
      isMobile
        ? // Актуально только для мобильной версии
          isMenuOpen
          ? // Если меню открыто, показываем его с анимацией
            'transform translate-y-0 shadow-lg'
          : // Если меню закрыто, скрываем его с анимацией
            'transform -translate-y-full'
        : // Для десктопной версии просто показываем меню
          '',
    ]"
  >
    <li v-for="item in navItems" :key="item.id" class="mb-4 md:mb-0">
      <a
        :href="item.path"
        class="text-primary hover:text-primary-light transition-colors duration-300 block py-2 md:py-0"
      >
        {{ $t(item.name) }}
      </a>
    </li>
  </ul>
</template>

<style lang="css" scoped>
ul {
  font-size: clamp(16px, 2vw, 22px);
}
</style>
