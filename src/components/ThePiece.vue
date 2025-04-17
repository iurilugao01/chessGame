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
  pieceCode: string;
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
      const ghosts: string[] = [];

      const moves = [];
      const moveUp = props.position[0] + (Number(props.position[1]) + 1);
      const moveDown = props.position[0] + (Number(props.position[1]) - 1);
      const moveRight = String.fromCharCode(
        props.position[0].charCodeAt(0) + 1
      );
      const moveLeft = String.fromCharCode(props.position[0].charCodeAt(0) - 1);
      const horizontalUpRight = moveRight[0] + moveUp[1];
      const horizontalUpLeft = moveLeft[0] + moveUp[1];
      const horizontalDownRight = moveRight[0] + moveDown[1];
      const horizontalDownLeft = moveLeft[0] + moveDown[1];

      moves.push(
        moveUp,
        moveDown,
        moveRight,
        moveLeft,
        horizontalUpRight,
        horizontalUpLeft,
        horizontalDownRight,
        horizontalDownLeft
      );
      moves.forEach((el) => {
        if (props.table[el][0] != props.pieceCode[0]) ghosts.push(el);
      });

      return ghosts;
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
      const ghosts: string[] = [];

      for (let i = 1; i <= 8; i++) {
        const index =
          String.fromCharCode(props.position[0].charCodeAt(0) + i) +
          (Number(props.position[1]) + i);

        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }
      for (let i = 1; i <= 8; i++) {
        const index =
          String.fromCharCode(props.position[0].charCodeAt(0) - i) +
          (Number(props.position[1]) + i);

        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }
      for (let i = 1; i <= 8; i++) {
        const index =
          String.fromCharCode(props.position[0].charCodeAt(0) + i) +
          (Number(props.position[1]) - i);

        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }
      for (let i = 1; i <= 8; i++) {
        const index =
          String.fromCharCode(props.position[0].charCodeAt(0) - i) +
          (Number(props.position[1]) - i);

        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }

      return ghosts;
    },
  },
  T: {
    name: "Tower",
    images: {
      white: "src/assets/images/wTower.svg",
      black: "src/assets/images/bTower.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];

      for (let i = 1; i <= 8; i++) {
        const index = props.position[0] + (Number(props.position[1]) + i);
        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }
      for (let i = 1; i <= 8; i++) {
        const index = props.position[0] + (Number(props.position[1]) - i);
        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }
      for (let i = 1; i <= 8; i++) {
        const index =
          String.fromCharCode(props.position[0].charCodeAt(0) + i) +
          props.position[1];
        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
      }
      for (let i = 1; i <= 8; i++) {
        const index =
          String.fromCharCode(props.position[0].charCodeAt(0) - i) +
          props.position[1];
        if (props.table[index][0] == props.pieceCode[0]) break;
        if (
          props.table[index][0] != props.pieceCode[0] &&
          props.table[index] != null
        ) {
          ghosts.push(index);
          break;
        }
        ghosts.push(index);
      }
      return ghosts;
    },
  },
  P: {
    name: "Pawn",
    images: {
      white: "src/assets/images/wPawn.svg",
      black: "src/assets/images/bPawn.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];
      console.log(props.table.C7);

      if (
        (props.pieceCode[0] === "w" && props.tableOrder == 1) ||
        (props.pieceCode[0] === "b" && props.tableOrder == 2)
      ) {
        const moveUp = props.position[0] + (Number(props.position[1]) + 1);
        if (props.table[moveUp] == null) ghosts.push(moveUp);

        const diagonalLeft = String.fromCharCode(moveUp[0].charCodeAt(0) - 1);
        if (diagonalLeft[0] != props.pieceCode[0] && diagonalLeft != null)
          ghosts.push(diagonalLeft);

        const diagonalRight = String.fromCharCode(moveUp[0].charCodeAt(0) + 1);
        if (diagonalRight[0] != props.pieceCode[0] && diagonalRight != null)
          ghosts.push(diagonalRight);

        if (props.position[1] === "2") {
          const move2 = String(
            props.position[0] + Number(props.position[1]) + 2
          );
          if (props.table[move2] == null) ghosts.push(move2);
        }
      }
      if (
        (props.pieceCode[0] === "b" && props.tableOrder == 1) ||
        (props.pieceCode[0] === "w" && props.tableOrder == 2)
      ) {
        const moveUp = Number(props.position[1]) - 1;
        if (props.table[moveUp] == null)
          ghosts.push(String(props.position[0] + moveUp));
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
