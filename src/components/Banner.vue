<template>
	<div class="banner">
		<h1>Make Your Burger</h1>
	</div>
</template>

<script setup></script>

<style scoped>
.banner {
	background-image: url('/src/assets/burger.jpg');
	background-position: center;
	background-size: cover;
	background-repeat: no-repeat;
	height: 500px;

	display: flex;
	align-items: center;
	justify-content: flex-start;
}

.banner h1 {
	color: #fff;
	text-align: center;
	font-size: 60px;
	background: #222;
	padding: 20px 40px;
}
</style>
