<script setup lang="ts">
// Определяем пропсы для компонента
defineProps({
  isOpen: {
    type: Boolean,
    required: true,
  },
});

// Определяем события
defineEmits(["click"]);
</script>

<template>
  <button
    class="relative w-8 h-8 flex flex-col justify-center items-center focus:outline-none"
    @click="$emit('click')"
    aria-label="Меню"
  >
    <!-- Три полоски, которые превращаются в крестик -->
    <div class="w-6 h-5 relative">
      <!-- Верхняя полоска -->
      <span
        class="absolute top-0 left-0 w-full h-0.5 bg-text rounded-sm transition-all origin-[left_center] duration-300"
        :class="isOpen ? 'rotate-45' : ''"
      ></span>

      <!-- Средняя полоска -->
      <span
        class="absolute top-2 left-0 w-full h-0.5 bg-text rounded-sm transition-opacity duration-300"
        :class="isOpen ? 'opacity-0' : ''"
      ></span>

      <!-- Нижняя полоска -->
      <span
        class="absolute top-4 left-0 w-full h-0.5 bg-text rounded-sm transition-all origin-[left_center] duration-300"
        :class="isOpen ? '-rotate-45' : ''"
      ></span>
    </div>
  </button>
</template>
