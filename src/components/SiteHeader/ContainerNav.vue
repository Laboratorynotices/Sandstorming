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
    // чтобы избежать дёргания при переходе
    hideMenu.value = true;
    setTimeout(() => {
      hideMenu.value = false;
    }, 300); // Время задержки перед показом меню

    /*
    Альтернативно можно попробвать:
    - Скрыть блок с меню (display: none),
    - Отключить анимацию,
    - Показать блок с меню (display: block),
    - Включить анимацию.
    */
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
  <nav class="nav-container flex justify-between items-center w-full">
    <!-- Навигационное меню -->
    <!-- Левая часть - кнопка-гамбургер и/или навигация -->
    <div class="flex items-center relative">
      <!-- Кнопка-гамбургер (видна только на мобильных) -->
      <BurgerButton :is-open="isMenuOpen" @click="toggleMenu" />

      <!-- Контейнер для навигации, который адаптируется
           в зависимости от текущего режима (мобильный/десктоп) -->
      <NavLinks
        :hideMenu="hideMenu"
        :isMobile="isMobile"
        :isMenuOpen="isMenuOpen"
        @link-clicked="closeMenu"
      />
    </div>

    <!-- Правая часть - Кнопка телефонного звонка -->
    <div>Телефон</div>
  </nav>
</template>
