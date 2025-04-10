<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import NavLinks from "./NavLinks.vue";
import BurgerButton from "./BurgerButton.vue";

// Состояние для отслеживания открытия/закрытия мобильного меню
const isMenuOpen = ref(false);

// Функция для переключения состояния мобильного меню
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

// Функция для закрытия меню
const closeMenu = () => {
  isMenuOpen.value = false;
};

// Функция для определения текущего размера экрана
const checkScreenSize = () => {
  // Если переходим на десктоп с открытым мобильным меню, закрываем его
  if (window.innerWidth >= 768 && isMenuOpen.value) {
    isMenuOpen.value = false;
  }
};

// Обработчик клика вне меню для его закрытия
const handleClickOutside = (event: MouseEvent) => {
  const navElement = document.getElementById("mobile-nav");
  const burgerButton = document.getElementById("burger-button");

  if (isMenuOpen.value && navElement && burgerButton) {
    if (
      !navElement.contains(event.target as Node) &&
      !burgerButton.contains(event.target as Node)
    ) {
      closeMenu();
    }
  }
};

// Установка слушателей событий при монтировании компонента
onMounted(() => {
  window.addEventListener("resize", checkScreenSize);
  document.addEventListener("click", handleClickOutside);
});

// Удаление слушателей событий при уничтожении компонента
onUnmounted(() => {
  window.removeEventListener("resize", checkScreenSize);
  document.removeEventListener("click", handleClickOutside);
});
</script>

<template>
  <nav class="flex justify-between items-center w-full">
    <!-- Левая часть - меню или кнопка-гамбургер -->
    <div class="flex items-center">
      <!-- Мобильная версия: кнопка-гамбургер -->
      <div id="burger-button" class="md:hidden z-20">
        <BurgerButton :is-open="isMenuOpen" @click="toggleMenu" />
      </div>

      <!-- Десктопная версия: горизонтальное меню -->
      <div class="hidden md:block">
        <NavLinks />
      </div>
    </div>

    <!-- Правая часть - кнопка для звонка -->
    <div>
      <button
        class="px-4 py-2 rounded border border-primary text-primary hover:bg-primary hover:text-white transition duration-300"
      >
        Позвонить
      </button>
    </div>

    <!-- Мобильное меню -->
    <div
      id="mobile-nav"
      class="fixed inset-x-0 top-0 z-10 bg-white transition-transform duration-300"
      :class="
        isMenuOpen
          ? 'transform translate-y-0 shadow-lg'
          : 'transform -translate-y-full'
      "
    >
      <div class="pt-16 p-4">
        <NavLinks @link-clicked="closeMenu" />
      </div>
    </div>
  </nav>
</template>
