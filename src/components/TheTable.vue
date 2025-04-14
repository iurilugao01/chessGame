<script setup lang="ts">
const positions: Record<number, string> = {
  1: "A",
  2: "B",
  3: "C",
  4: "D",
  5: "E",
  6: "F",
  7: "G",
  8: "H",
};

function usePosition(value: number): string {
  const position = positions[value];
  if (!position) throw new Error(`Invalid value: ${value}`);
  return position;
}
</script>

<template>
  <table class="table-auto">
    <tbody>
      <tr>
        <td class="p-3 bg-amber-950"></td>
        <td class="p-3 bg-amber-950" v-for="col in 8" :key="col">
          {{ usePosition(col) }}
        </td>
      </tr>
      <tr v-for="row in 8" :key="row">
        <td class="p-3 bg-amber-950">{{ row }}</td>
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
