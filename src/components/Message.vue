<template>
	<div class="message-container">
		<p>{{ msg }}</p>
	</div>
</template>

<script setup>
const props = defineProps({
	msg: String
})
</script>

<style scoped>
.message-container {
	color: #004085;
	background: #cce5ff;
	border: 2px solid #b8daff;
	border-radius: 6px;
	padding: 10px;
	width: 100%;
	margin: 30px auto;
}
</style>
