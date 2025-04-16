<script setup lang="ts">
function usePosition(value: number): string {
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
  const position = positions[value];
  if (!position) throw new Error(`Invalid value: ${value}`);
  return position;
}
defineExpose({
  usePosition,
});
</script>

<template>
  <table class="table-auto">
    <tbody>
      <tr>
        <td class="h-12 w-12 text-center bg-amber-950"></td>
        <td
          class="h-12 w-12 text-center bg-amber-950"
          v-for="col in 8"
          :key="col"
        >
          {{ usePosition(col) }}
        </td>
      </tr>
      <tr v-for="row in 8" :key="row">
        <td class="h-12 w-12 text-center bg-amber-950">{{ row }}</td>
        <td
          v-for="col in 8"
          :class="{
            'h-12 w-12 text-center': true,
            'bg-white': (row + col) % 2,
            'bg-black': !((row + col) % 2),
          }"
        >
          <slot :name="usePosition(col) + row"> </slot>
        </td>
      </tr>
    </tbody>
  </table>
</template>
