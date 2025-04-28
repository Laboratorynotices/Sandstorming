<script setup lang="ts">
// Перечисление социальных сетей
const socialNetworks = [
  { name: "Facebook", fileName: "Facebook_black.svg", url: "#" },
  { name: "Instagram", fileName: "Instagram_black.svg", url: "#" },
  { name: "YouTube", fileName: "Youtube_black.svg", url: "#" },
  { name: "WhatsApp", fileName: "WhatsApp_black.svg", url: "#" },
].map((socialNetwork) => ({
  ...socialNetwork,
  src: new URL(`../../assets/images/${socialNetwork.fileName}`, import.meta.url)
    .href,
}));
</script>
<template>
  <ul class="inline-flex flex-wrap gap-[10px_18px] mt-2">
    <li v-for="(network, index) in socialNetworks" :key="index">
      <a
        :href="network.url"
        target="_blank"
        rel="noopener noreferrer"
        class="bg-background p-0.5 block rounded-full"
      >
        <img
          :src="network.src"
          :alt="$t(network.name)"
          :title="$t(network.name)"
          class="inline-block h-[53px] aspect-square"
        />
      </a>
    </li>
  </ul>
</template>
