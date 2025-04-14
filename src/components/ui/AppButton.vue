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
const baseClasses = "rounded-full items-center";

// Классы для конкретного варианта кнопки
const variantClasses = computed(() => {
  switch (props.variant) {
    case ButtonVariant.Call:
      return "bg-primary gap-2.5 text-background flex font-bold call";
    case ButtonVariant.Header1:
      return "bg-text text-background header1";
    case ButtonVariant.Header2:
      return "bg-muted text-primary border-primary border-1 px-5 py-2.5 inline-block header2";
    case ButtonVariant.Event1:
      return "bg-text text-background uppercase font-extrabold event1";
    case ButtonVariant.Event2:
      return "bg-overlay text-text border-text border-1 uppercase font-extrabold event2";
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
  padding: clamp(6px, 1vw, 10px) clamp(12px, 2vw, 20px);
}
.header1 {
  font-size: clamp(12px, 2vw, 14px);
  padding: clamp(2px, 1vw, 4px) clamp(4px, 2vw, 8px);
}
.event1 {
  font-size: clamp(15px, 2.5vw, 32px);
  padding: clamp(6px, 1.5vw, 10px) clamp(12px, 2.5vw, 20px);
}
.event2 {
  font-size: clamp(15px, 2.5vw, 32px);
  padding: clamp(6px, 1.5vw, 10px) clamp(12px, 2.5vw, 20px);
}
</style>
