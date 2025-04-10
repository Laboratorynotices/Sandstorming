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
  <div id="burger-button" class="md:hidden z-20">
    <button
      class="relative w-8 h-8 flex flex-col justify-center items-center focus:outline-none"
      aria-label="Меню"
    >
      <!-- Три полоски, которые превращаются в крестик -->
      <div class="w-6 h-6 flex flex-col justify-between">
        <!-- Верхняя полоска -->
        <span
          class="h-0.5 bg-text rounded-sm transition-all origin-[left_center] duration-300"
          :class="isOpen ? 'rotate-45 w-[130%]' : 'w-full'"
        ></span>

        <!-- Средняя полоска -->
        <span
          class="w-full h-0.5 bg-text rounded-sm transition-opacity duration-300"
          :class="isOpen ? 'opacity-0' : ''"
        ></span>

        <!-- Нижняя полоска -->
        <span
          class="h-0.5 bg-text rounded-sm transition-all origin-[left_center] duration-300"
          :class="isOpen ? '-rotate-45 w-[130%]' : 'w-full'"
        ></span>
      </div>
    </button>
  </div>
</template>
