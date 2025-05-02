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
  pieceCode: string;
  position: string;
  table: Record<string, string | null>;
  tableOrder: number;
  turn: boolean;
}>();

const isValidSquare = (pos: string): boolean => {
  if (pos.length !== 2) return false;
  const cell = props.table[pos];
  if (cell && cell[0] === props.pieceCode[0]) return false;
  const collum = pos.charCodeAt(0);
  const position = Number(pos[1]);
  return collum >= 65 && collum <= 72 && position >= 1 && position <= 8;
};
const isValidTarget = (pos: string): boolean => {
  const cell = props.table[pos];
  if (cell && cell[0] !== props.pieceCode[0]) return true;
  return false;
};
const pieces: Record<string, PieceKey> = {
  K: {
    name: "King",
    images: {
      white: "/wKing.svg",
      black: "/bKing.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];
      const [collum, rankChar] = props.position;
      const rank = Number(rankChar);
      const deltas = [
        [0, 1],
        [0, -1],
        [1, 0],
        [-1, 0],
        [1, 1],
        [-1, 1],
        [1, -1],
        [-1, -1],
      ];
      for (const [dc, dr] of deltas) {
        const newCollum = String.fromCharCode(collum.charCodeAt(0) + dc);
        const newRank = (rank + dr).toString();
        const index = newCollum + newRank;
        if (isValidSquare(index)) ghosts.push(index);
      }
      return ghosts;
    },
  },
  Q: {
    name: "Queen",
    images: {
      white: "/wQueen.svg",
      black: "/bQueen.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];

      ghosts.push(...pieces.B.showMoves());
      ghosts.push(...pieces.T.showMoves());

      return ghosts;
    },
  },
  H: {
    name: "Horse",
    images: {
      white: "/wHorse.svg",
      black: "/bHorse.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];
      const [collum, rankChar] = props.position;
      const rank = Number(rankChar);
      const directions = [
        [2, 0],
        [0, 2],
        [-2, 0],
        [0, -2],
      ];
      for (const [dc, dr] of directions) {
        const newCollum = String.fromCharCode(collum.charCodeAt(0) + dc);
        const newRank = rank + dr;
        const movL1 = [
          newCollum + String(newRank + 1),
          newCollum + String(newRank - 1),
        ];
        const movL2 = [
          String.fromCharCode(newCollum.charCodeAt(0) + 1) + String(newRank),
          String.fromCharCode(newCollum.charCodeAt(0) - 1) + String(newRank),
        ];

        const index = dr == 0 ? movL1 : movL2;
        index.forEach((el) => {
          if (isValidSquare(el)) ghosts.push(el);
        });
      }
      return ghosts;
    },
  },
  B: {
    name: "Bishop",
    images: {
      white: "/wBishop.svg",
      black: "/bBishop.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];
      const [collum, rankChar] = props.position;
      const rank = Number(rankChar);
      const directions = [
        [1, 1],
        [-1, 1],
        [1, -1],
        [-1, -1],
      ];
      for (const [dc, dr] of directions) {
        for (let i = 1; i <= 8; i++) {
          const newCollum = String.fromCharCode(collum.charCodeAt(0) + dc * i);
          const newRank = (rank + dr * i).toString();
          const index = newCollum + newRank;
          if (!isValidSquare(index)) break;
          if (isValidTarget(index)) {
            ghosts.push(index);
            break;
          }
          ghosts.push(index);
        }
      }
      return ghosts;
    },
  },
  T: {
    name: "Tower",
    images: {
      white: "/wTower.svg",
      black: "/bTower.svg",
    },
    showMoves: () => {
      const ghosts: string[] = [];
      const [collum, rankChar] = props.position;
      const rank = Number(rankChar);
      const directions = [
        [0, 1],
        [0, -1],
        [1, 0],
        [-1, 0],
      ];
      for (const [dc, dr] of directions) {
        for (let i = 1; i <= 8; i++) {
          const newCollum = String.fromCharCode(collum.charCodeAt(0) + dc * i);
          const newRank = (dr === 0 ? rank : rank + dr * i).toString();
          const index = newCollum + newRank;
          if (!isValidSquare(index)) break;
          if (isValidTarget(index)) {
            ghosts.push(index);
            break;
          }
          ghosts.push(index);
        }
      }
      return ghosts;
    },
  },
  P: {
    name: "Pawn",
    images: {
      white: "/wPawn.svg",
      black: "/bPawn.svg",
    },
    showMoves: () => {
      const tableSide = (): boolean => {
        if (
          (props.pieceCode[0] === "w" && props.tableOrder == 1) ||
          (props.pieceCode[0] === "b" && props.tableOrder == 2)
        ) {
          return true;
        }
        return false;
      };
      const isUp = tableSide();

      const ghosts: string[] = [];
      const [collum, rankChar] = props.position;
      const rank = Number(rankChar);

      const forward1 = isUp ? 1 : -1;
      const nextRank1 = collum + (rank + forward1).toString();
      console.log("nextRank1: " + nextRank1);
      if (isValidSquare(nextRank1) && !isValidTarget(nextRank1))
        ghosts.push(nextRank1);

      const forward2 = isUp ? 2 : -2;
      if ([2, 7].includes(rank)) {
        const nextRank2 = collum + (rank + forward2).toString();
        if (isValidSquare(nextRank2) && !isValidTarget(nextRank2))
          ghosts.push(nextRank2);
      }

      for (const df of [-1, 1]) {
        const newCollum = String.fromCharCode(collum.charCodeAt(0) + df);
        const diagonal = newCollum + (rank + forward1).toString();

        console.log(diagonal);
        if (isValidSquare(diagonal) && isValidTarget(diagonal))
          ghosts.push(diagonal);
      }

      return ghosts;
    },
  },
};

const checkTurn = (): boolean =>
  (props.pieceCode[0] === "w" && props.turn) ||
  (props.pieceCode[0] === "b" && !props.turn);
</script>

<template>
  <img
    :src="
      pieceCode[0] === 'w'
        ? pieces[pieceCode[1]].images.white
        : pieces[pieceCode[1]].images.black
    "
    @click="
      checkTurn()
        ? $emit('onfocus', pieceCode, pieces[pieceCode[1]].showMoves())
        : null
    "
    :class="{
      'cursor-pointer': checkTurn,
    }"
    :alt="pieces[pieceCode[1]].name"
  />
</template>
