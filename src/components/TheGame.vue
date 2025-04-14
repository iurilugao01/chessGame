<script setup lang="ts">
type pieceKey = {
  king: boolean;
  queen: boolean;
  horses: { h1: boolean; h2: boolean };
  bishops: { b1: boolean; b2: boolean };
  towers: { t1: boolean; t2: boolean };
  pawns: {
    p1: boolean;
    p2: boolean;
    p3: boolean;
    p4: boolean;
    p5: boolean;
    p6: boolean;
    p7: boolean;
    p8: boolean;
  };
};

const table: Record<string, string | null> = {
  A1: "wT1",
  B1: "wH1",
  C1: "wB1",
  D1: "wQ1",
  E1: "wK1",
  F1: "wB2",
  G1: "wH2",
  H1: "wT2",
  A2: "wP1",
  B2: "wP2",
  C2: "wP3",
  D2: "wP4",
  E2: "wP5",
  F2: "wP6",
  G2: "wP7",
  H2: "wP8",
  A3: null,
  B3: null,
  C3: null,
  D3: null,
  E3: null,
  F3: null,
  G3: null,
  H3: null,
  A4: null,
  B4: null,
  C4: null,
  D4: null,
  E4: null,
  F4: null,
  G4: null,
  H4: null,
  A5: null,
  B5: null,
  C5: null,
  D5: null,
  E5: null,
  F5: null,
  G5: null,
  H5: null,
  A6: null,
  B6: null,
  C6: null,
  D6: null,
  E6: null,
  F6: null,
  G6: null,
  H6: null,
  A7: "bP1",
  B7: "bP2",
  C7: "bP3",
  D7: "bP4",
  E7: "bP5",
  F7: "bP6",
  G7: "bP7",
  H7: "bP8",
  A8: "bT1",
  B8: "bH1",
  C8: "bB1",
  D8: "bQ1",
  E8: "bK1",
  F8: "bB2",
  G8: "bH2",
  H8: "bT2",
};
const wPieces: pieceKey = {
  king: true,
  queen: true,
  horses: { h1: true, h2: true },
  bishops: { b1: true, b2: true },
  towers: { t1: true, t2: true },
  pawns: {
    p1: true,
    p2: true,
    p3: true,
    p4: true,
    p5: true,
    p6: true,
    p7: true,
    p8: true,
  },
};
const bPieces: pieceKey = {
  king: true,
  queen: true,
  horses: { h1: true, h2: true },
  bishops: { b1: true, b2: true },
  towers: { t1: true, t2: true },
  pawns: {
    p1: true,
    p2: true,
    p3: true,
    p4: true,
    p5: true,
    p6: true,
    p7: true,
    p8: true,
  },
};

const movePiece = (targetPiece: string, targetPosition: string): void => {
  const oldPosition = () => {
    for (const piece in table) {
      if (targetPiece === table[piece]) return piece;
    }
  };
  table.oldPosition = null;
  table.targetPosition = targetPiece;
};
</script>

<template></template>
