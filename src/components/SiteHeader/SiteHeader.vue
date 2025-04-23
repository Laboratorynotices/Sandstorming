<script setup lang="ts">
import ContainerNav from "./ContainerNav.vue";
import HeaderTitle from "./HeaderTitle.vue";
import HeaderElements from "./HeaderElements.vue";
</script>

<template>
  <header id="site-header">
    <div id="header-background-transparent"></div>
    <div class="wrap-container">
      <ContainerNav />
      <HeaderTitle />
      <HeaderElements />
    </div>
  </header>
</template>
