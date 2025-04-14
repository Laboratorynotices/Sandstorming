<script setup lang="ts">
import SchoolBenefits from "./SchoolBenefits.vue";
import SchoolLocation from "./SchoolLocation.vue";
import HeaderEvents from "./HeaderEvents.vue";
import SocialNetworks from "./SocialNetworks.vue";
</script>

<template>
  <div
    class="header_elements_container md:grid md:grid-cols-[1fr_1fr] md:grid-rows-[auto_1fr_auto]"
  >
    <SchoolLocation class="item-a" />
    <HeaderEvents class="item-b" />
    <SchoolBenefits class="item-d" />
    <SocialNetworks class="item-e" />
  </div>
</template>

<style lang="css" scoped>
/* Десктопная версия с привязками элементов */
@media (min-width: 768px) {
  .header_elements_container {
    grid-template-areas:
      "a b"
      "d b"
      "e b";
  }
}

.item-a {
  grid-area: a;
}
.item-b {
  grid-area: b;
}
.item-d {
  grid-area: d;
}
.item-e {
  grid-area: e;
}
</style>
