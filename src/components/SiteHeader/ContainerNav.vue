<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import NavLinks from "./NavLinks.vue";
import BurgerButton from "./BurgerButton.vue";

// Ширина экрана для MD версии
// @TODO: вынести в конфиг и "привязать" в настройках tailwind
const MD_BREAKPOINT = 768;

// Состояние для отслеживания открытия/закрытия мобильного меню
const isMenuOpen = ref(false);
// Состояние для отслеживания видимости меню (для перехода из десктопа в мобильный)
const hideMenu = ref(false);
// Флаг для отслеживания текущего состояния отображения (мобильное/десктопное)
const isMobile = ref(window.innerWidth < MD_BREAKPOINT);

// Функция для переключения состояния мобильного меню
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

// Функция для закрытия меню
const closeMenu = () => {
  if (isMenuOpen.value) {
    isMenuOpen.value = false;
  }
};

// Функция для определения текущего размера экрана
const checkScreenSize = () => {
  const wasMobile = isMobile.value;
  isMobile.value = window.innerWidth < MD_BREAKPOINT;

  // Если переходим с мобильного на десктоп с открытым мобильным меню, закрываем его
  if (wasMobile && !isMobile.value && isMenuOpen.value) {
    isMenuOpen.value = false;
  }

  if (!wasMobile && isMobile.value) {
    // Если переходим с десктопа на мобильный, скрываем меню на пару секунд
    hideMenu.value = true;
    setTimeout(() => {
      hideMenu.value = false;
    }, 300); // Время задержки перед показом меню
  }
};

// Обработчик клика вне меню для его закрытия
const handleClickOutside = (event: MouseEvent) => {
  const navElement = document.getElementById("nav-container");
  const burgerButton = document.getElementById("burger-button");

  if (isMenuOpen.value && isMobile.value && navElement && burgerButton) {
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
  checkScreenSize(); // Проверяем начальное состояние
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
    <!-- Левая часть - кнопка-гамбургер и/или навигация -->
    <div class="flex items-center relative">
      <!-- Кнопка-гамбургер (видна только на мобильных) -->
      <div id="burger-button" class="md:hidden z-20">
        <BurgerButton :is-open="isMenuOpen" @click="toggleMenu" />
      </div>

      <!-- Общий контейнер для навигации, который адаптируется
           в зависимости от текущего режима (мобильный/десктоп) -->
      <div
        id="nav-container"
        :class="[
          // Базовые стили применяются всегда
          '',

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
        <!-- Навигационные ссылки (один компонент для обоих режимов) -->
        <NavLinks @link-clicked="closeMenu" />
      </div>
    </div>

    <!-- Правая часть - кнопка для звонка -->
    <div>
      <button
        class="px-4 py-2 rounded border border-primary text-primary hover:bg-primary hover:text-background transition duration-300"
      >
        Позвонить
      </button>
    </div>
  </nav>
</template>
