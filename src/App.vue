<script setup lang="ts">
import CanvasBoard from "./components/CanvasBoard.vue";
</script>

<template>
	<CanvasBoard />
</template>

<style>
*,
::before,
::after {
	box-sizing: border-box;
	padding: 0;
	margin: 0;
}

html,
body,
#app {
	width: 100%;
	height: 100%;
	padding: 0;
	margin: 0;
}
</style>
