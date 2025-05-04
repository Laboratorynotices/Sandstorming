<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import { ButtonVariant } from "../../constants/button";
import AppButton from "../ui/AppButton.vue";
import NavLinks from "./NavLinks.vue";
import BurgerButton from "./BurgerButton.vue";
import SwitchLocale from "./SwitchLocale.vue";
import { useWindowInnerWidthRem } from "../../composables/useWindowInnerWidthRem";

// Получаем ширину окна в rem
const { windowWidthRem } = useWindowInnerWidthRem();

// Ширина экрана для MD версии
// Получаем доступ к константе через import.meta.env
const MD_BREAKPOINT: number = import.meta.env.MD_BREAKPOINT;

// Состояние для отслеживания открытия/закрытия мобильного меню
const isMenuOpen = ref(false);
// Состояние для отслеживания видимости меню (для перехода из десктопа в мобильный)
const hideMenu = ref(false);
// Флаг для отслеживания текущего состояния отображения (мобильное/десктопное)
const isMobile = ref(true);
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
  isMobile.value = windowWidthRem.value < MD_BREAKPOINT;

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
  const navContainer = ref<HTMLElement | null>(null);
  // На ref поменять нельзя, поскольку он должен будет ссылаться на дочерний элемент
  const burgerButton = document.getElementById("burger-button");

  // Проверяем, что клик был вне меню и кнопки-гамбургера
  // и что меню открыто и мы на мобильном устройстве
  if (isMenuOpen.value && isMobile.value && navContainer && burgerButton) {
    // Если клик был вне меню и кнопки-гамбургера, закрываем меню
    if (
      !navContainer.value?.contains(event.target as Node) &&
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
  <nav
    ref="navContainer"
    class="nav-container flex justify-between items-center w-full"
  >
    <!-- Навигационное меню -->
    <!-- Левая часть - кнопка-гамбургер и/или навигация -->
    <div class="flex items-center relative">
      <!-- Кнопка-гамбургер (видна только на мобильных) -->
      <BurgerButton
        ref="burgerButton"
        :is-open="isMenuOpen"
        @click="toggleMenu"
      />

      <!-- Контейнер для навигации, который адаптируется
           в зависимости от текущего режима (мобильный/десктоп) -->
      <NavLinks
        :hideMenu="hideMenu"
        :isMobile="isMobile"
        :isMenuOpen="isMenuOpen"
        @link-clicked="closeMenu"
      />
    </div>

    <!-- Правая часть -->
    <div class="flex items-center gap-4">
      <!-- Переключатель языков -->
      <AppButton :variant="ButtonVariant.Call">
        <SwitchLocale />
      </AppButton>
      <!-- Кнопка телефонного звонка -->
      <AppButton :variant="ButtonVariant.Call" href="tel:+201001234567">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="2.5"
          stroke="currentColor"
          width="1em"
          height="1em"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z"
          ></path>
        </svg>
        <span class="whitespace-nowrap">+20 100 123 4567</span>
      </AppButton>
    </div>
  </nav>
</template>
