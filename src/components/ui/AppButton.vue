<script setup lang="ts">
import { computed } from "vue";
import { ButtonVariant } from "../../constants/button";
import type { AppButtonProps } from "../../types/button";

const props = defineProps<AppButtonProps>();

// Проверка: если href задан, то as должен быть либо 'a', либо не задан вообще
if (props.href && props.as && props.as !== "a") {
  throw new Error(
    `[AppButton] Invalid props: when "href" is provided, "as" must be "a" or undefined (got "${props.as}")`,
  );
}

const asComputed = computed(() => {
  if (props.as) return props.as;
  if (props.href) return "a";
  return "span";
});

// Общие классы для всех вариантов кнопки
const baseClasses = "px-2 rounded-full flex items-center";

// Классы для конкретного варианта кнопки
const variantClasses = computed(() => {
  switch (props.variant) {
    case ButtonVariant.Call:
      return "bg-primary text-background font-bold call";
    default:
      return "";
  }
});
</script>

<template>
  <component
    :is="asComputed"
    :href="asComputed === 'a' ? href || '#' : undefined"
    :class="[baseClasses, variantClasses]"
  >
    <slot />
  </component>
</template>

<style lang="css">
.call {
  font-size: clamp(12px, 2vw, 20px);
}
</style>
