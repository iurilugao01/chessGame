<script setup lang="ts">
defineProps<{
  pieceToMove: string;
  newPosition: string;
}>();
</script>

<template>
  <div
    @click="$emit('movePiece', pieceToMove, newPosition)"
    class="cursor-pointer"
  >
    <div class="w-4 h-4 rounded-full opacity-75 bg-gray-600 m-auto"></div>
  </div>
</template>
