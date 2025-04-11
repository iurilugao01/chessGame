<script setup lang="ts"></script>

<template>
  <table class="table-auto">
    <tbody>
      <tr v-for="row in 8" :key="row" class="border-b border-gray-200">
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
