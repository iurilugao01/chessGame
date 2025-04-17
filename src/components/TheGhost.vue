<script setup lang="ts">
defineProps<{
  pieceToMove: string;
  newPosition: string;
}>();
</script>

<template>
  <div
    @click="$emit('movePiece', pieceToMove, newPosition)"
    class="absolute inset-0 flex items-center justify-center z-10 p-2 cursor-pointer"
  >
    <div class="w-4 h-4 rounded-full opacity-75 bg-gray-600 m-auto"></div>
  </div>
</template>
