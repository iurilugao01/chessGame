<script setup lang="ts">
type PieceKey = {
  name: string;
  images: {
    white: string;
    black: string;
  };
  showMoves: () => string[];
};

const props = defineProps<{
  pieceCode: string | null;
  position: string;
  turn: boolean;
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
    showMoves: () => {
      const ghosts = [];
      const value = Number(props.position[1]) + 1;
      ghosts.push(string(props.position[0] + value));
      return ghosts;
    },
  },
};
</script>

<template>
  <img
    :src="
      pieceCode[0] === 'w'
        ? pieces[pieceCode[1]].images.white
        : pieces[pieceCode[1]].images.black
    "
    @click="$emit('onfocus', pieceCode)"
    :alt="pieces[pieceCode[1]].name"
    v-if="pieceCode"
  />
</template>
