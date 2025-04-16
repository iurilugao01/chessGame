<script setup lang="ts">
import { onMounted } from "vue";

type PieceKey = {
  name: string;
  images: {
    white: string;
    black: string;
  };
  showMoves: () => void;
};

const props = defineProps<{
  pieceType: string | null;
}>();

const pieces: Record<string, PieceKey> = {
  K: {
    name: "King",
    images: {
      white: "src/assets/images/wKing.svg",
      black: "src/assets/images/bKing.svg",
    },
    showMoves: () => {},
  },
  Q: {
    name: "Queen",
    images: {
      white: "src/assets/images/wQueen.svg",
      black: "src/assets/images/bQueen.svg",
    },
    showMoves: () => {},
  },
  H: {
    name: "Horse",
    images: {
      white: "src/assets/images/wHorse.svg",
      black: "src/assets/images/bHorse.svg",
    },
    showMoves: () => {},
  },
  B: {
    name: "Bishop",
    images: {
      white: "src/assets/images/wBishop.svg",
      black: "src/assets/images/bBishop.svg",
    },
    showMoves: () => {},
  },
  T: {
    name: "Tower",
    images: {
      white: "src/assets/images/wTower.svg",
      black: "src/assets/images/bTower.svg",
    },
    showMoves: () => {},
  },
  P: {
    name: "Pawn",
    images: {
      white: "src/assets/images/wPawn.svg",
      black: "src/assets/images/bPawn.svg",
    },
    showMoves: () => {},
  },
};

onMounted(() => {
  console.log(props.pieceType);
});
</script>

<template>
  <img
    :src="
      pieceType[0] === 'w'
        ? pieces[pieceType[1]].images.white
        : pieces[pieceType[1]].images.black
    "
    :alt="pieces[pieceType[1]].name"
    v-if="pieceType"
  />
</template>
