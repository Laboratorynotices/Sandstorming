<script setup lang="ts">
import { ButtonVariant } from "../../constants/button";
import AppButton from "../ui/AppButton.vue";
</script>

<template>
  <AppButton :variant="ButtonVariant.Header1">{{
    $t("school location")
  }}</AppButton>
</template>
