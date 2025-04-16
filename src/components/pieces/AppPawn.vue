<script setup lang="ts">
import { defineProps } from "vue";
import bPawn from "@/assets/images/bPawn.png";

const props = defineProps<{
  onfocus: {
    type: string;
    default: false;
  };
  table: {
    type: Record<string, string>;
    required: true;
  };
}>();
</script>

<template>
  <img :src="bPawn" alt="Peão preto" />
</template>
