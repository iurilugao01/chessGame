<script setup lang="ts">
defineProps<{
  turn: boolean;
}>();

const images = {
  white: "src/assets/images/wKing.svg",
  black: "src/assets/images/bKing.svg",
};

const usePosition = (value: number): string =>
  String.fromCharCode("A".charCodeAt(0) + (value - 1));
</script>

<template>
  <table class="table-auto">
    <tbody>
      <tr>
        <td class="h-12 w-12 text-center bg-gray-900">
          <img
            :src="turn ? images.white : images.black"
            :alt="turn ? 'turno das peças brancas' : 'turno das peças pretas'"
          />
        </td>
        <td
          class="h-12 w-12 text-center bg-gray-900"
          v-for="col in 8"
          :key="col"
        >
          {{ usePosition(col) }}
        </td>
      </tr>
      <tr v-for="row in 8" :key="row">
        <td class="h-12 w-12 text-center bg-gray-900">{{ row }}</td>
        <td
          v-for="col in 8"
          :class="{
            'h-12 w-12 relative': true,
            'bg-white': (row + col) % 2,
            'bg-green-600': !((row + col) % 2),
          }"
        >
          <slot :name="usePosition(col) + row"> </slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>
