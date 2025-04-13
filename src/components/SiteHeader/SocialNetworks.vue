<script setup lang="ts">
// Перечисление социальных сетей
const socialNetworks = [
  { name: "Facebook", fileName: "Facebook_black.svg", url: "#" },
  { name: "Instagram", fileName: "Instagram_black.svg", url: "#" },
  { name: "YouTube", fileName: "Youtube_black.svg", url: "#" },
  { name: "WhatsApp", fileName: "WhatsApp_black.svg", url: "#" },
];
</script>
<template>
  <ul class="inline-flex flex-wrap gap-[10px_18px] mt-2">
    <li v-for="(network, index) in socialNetworks" :key="index">
      <img
        :src="`/src/assets/images/${network.fileName}`"
        :alt="$t(network.name)"
        :title="$t(network.name)"
        class="inline-block"
      />
    </li>
  </ul>
</template>
