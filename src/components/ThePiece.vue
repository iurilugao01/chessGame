<script setup lang="ts">
type PieceKey = {
  name: string;
  images: {
    white: string;
    black: string;
  };
  showMoves: () => string[] | undefined;
};

const props = defineProps<{
  pieceCode: string | null;
  position: string;
  table: Record<string, string>;
  tableOrder: number;
  turn: boolean;
}>();

const pieces: Record<string, PieceKey> = {
  K: {
    name: "King",
    images: {
      white: "src/assets/images/wKing.svg",
      black: "src/assets/images/bKing.svg",
    },
    showMoves: () => {
      return ["move"];
    },
  },
  Q: {
    name: "Queen",
    images: {
      white: "src/assets/images/wQueen.svg",
      black: "src/assets/images/bQueen.svg",
    },
    showMoves: () => {
      return ["move"];
    },
  },
  H: {
    name: "Horse",
    images: {
      white: "src/assets/images/wHorse.svg",
      black: "src/assets/images/bHorse.svg",
    },
    showMoves: () => {
      return ["move"];
    },
  },
  B: {
    name: "Bishop",
    images: {
      white: "src/assets/images/wBishop.svg",
      black: "src/assets/images/bBishop.svg",
    },
    showMoves: () => {
      return ["move"];
    },
  },
  T: {
    name: "Tower",
    images: {
      white: "src/assets/images/wTower.svg",
      black: "src/assets/images/bTower.svg",
    },
    showMoves: () => {
      return ["move"];
    },
  },
  P: {
    name: "Pawn",
    images: {
      white: "src/assets/images/wPawn.svg",
      black: "src/assets/images/bPawn.svg",
    },
    showMoves: () => {
      const ghosts = [];
      if (props.pieceCode == null) return;
      if (
        (props.pieceCode[0] === "w" && props.tableOrder == 1) ||
        (props.pieceCode[0] === "b" && props.tableOrder == 2)
      ) {
        const move1 = Number(props.position[1]) + 1;
        if (props.table[move1] == null)
          ghosts.push(String(props.position[0] + move1));

        if (props.position[1] === "2") {
          const move2 = Number(props.position[1]) + 2;
          if (props.table[move1] == null)
            ghosts.push(String(props.position[0] + move2));
        }
      }
      if (
        (props.pieceCode[0] === "b" && props.tableOrder == 1) ||
        (props.pieceCode[0] === "w" && props.tableOrder == 2)
      ) {
        const move1 = Number(props.position[1]) - 1;
        if (props.table[move1] == null)
          ghosts.push(String(props.position[0] + move1));
        if (props.position[1] === "7") {
          const move2 = Number(props.position[1]) - 2;
          if (props.table[move2] == null)
            ghosts.push(String(props.position[0] + move2));
        }
      }
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
    @click="$emit('onfocus', pieceCode, pieces[pieceCode[1]].showMoves())"
    :alt="pieces[pieceCode[1]].name"
    v-if="pieceCode"
  />
</template>
