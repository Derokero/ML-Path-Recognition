<script setup lang="ts">
import { onMounted, ref, useTemplateRef } from "vue";

const boardRef = useTemplateRef("board");
const board = ref(boardRef.value);
const ctx = ref<CanvasRenderingContext2D | null>();

const isDrawing = ref(false);

onMounted(() => {
	board.value = boardRef.value;
	ctx.value = board.value?.getContext("2d");
});

const setIsDrawing = (state: boolean) => {
	isDrawing.value = state;
};

const stopDrawing = () => {
	setIsDrawing(false);
	ctx.value?.beginPath();
};

const draw = (mouseEvent: MouseEvent) => {
	if (!board.value) return;
	if (!isDrawing.value) return;
	if (!ctx.value) return;

	ctx.value.lineWidth = 2;
	ctx.value.lineJoin = "round";
	ctx.value.lineTo(mouseEvent.offsetX, mouseEvent.offsetY);
	ctx.value.stroke();
};
</script>

<template>
	<canvas
		@mousedown.left="setIsDrawing(true)"
		@mouseup="stopDrawing"
		@mousemove="draw"
		ref="board"
		class="board"
		width="500"
		height="500"
	/>
</template>

<style scoped>
.board {
	aspect-ratio: 1/1;
	border: 2px solid peachpuff;
	margin-block-start: 10vh;
	margin-inline-start: 15vw;
}
</style>
