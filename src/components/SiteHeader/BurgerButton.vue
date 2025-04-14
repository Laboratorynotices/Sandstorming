<script setup lang="ts">
// Определяем пропсы для компонента
defineProps({
  isOpen: {
    type: Boolean,
    required: true,
  },
});
</script>

<template>
  <button
    id="burger-button"
    class="w-7.5 h-7.5 flex flex-col justify-between items-center focus:outline-none md:hidden z-20"
    :class="isOpen ? 'fixed' : 'relative'"
    aria-label="Меню"
  >
    <!-- Три полоски, которые превращаются в крестик -->
    <!-- Верхняя полоска -->
    <span
      class="h-0.5 bg-text rounded-sm transition-all origin-[left_center] duration-300"
      :class="isOpen ? 'rotate-45 w-[130%] ml-2' : 'w-full'"
    ></span>

    <!-- Средняя полоска -->
    <span
      class="h-0.5 bg-text rounded-sm transition-opacity duration-300"
      :class="isOpen ? 'opacity-0' : 'w-full'"
    ></span>

    <!-- Нижняя полоска -->
    <span
      class="h-0.5 bg-text rounded-sm transition-all origin-[left_center] duration-300"
      :class="isOpen ? '-rotate-45 w-[130%] ml-2' : 'w-full'"
    ></span>
  </button>
</template>
