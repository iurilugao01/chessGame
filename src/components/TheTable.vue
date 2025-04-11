<script setup lang="ts">
export function usePosition(value: string): number {
  switch (value.toUpperCase()) {
    case "A":
      return 1;
    case "B":
      return 2;
    case "C":
      return 3;
    case "D":
      return 4;
    case "E":
      return 5;
    case "F":
      return 6;
    case "G":
      return 7;
    case "H":
      return 8;
    default:
      return null;
  }
}
</script>

<template>
  <table class="table-auto">
    <tbody>
      <tr>
        <td></td>
        <td v-for="col in 8"></td>
      </tr>
      <tr v-for="row in 8" :key="row" class="border-b border-gray-200">
        <td class="p-3">{{ row }}</td>
        <td
          v-for="col in 8"
          :class="{
            'p-3': true,
            'bg-white': (row + col) % 2,
            'bg-black': !((row + col) % 2),
          }"
        ></td>
      </tr>
    </tbody>
  </table>
</template>
