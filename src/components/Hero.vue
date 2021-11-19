<template>
	<div class="hero">
		<div class="hero-img"></div>
		<parallax></parallax>
		<!-- <minting></minting> -->
		<!-- <div class="description-section"></div> -->
	</div>
</template>

<script>
// import Minting from "./Minting.vue";
import Parallax from "./Parallax.vue";
export default {
	components: {
		// Minting,
		Parallax,
	},
};
</script>

<style lang="scss">
.hero {
	width: 100%;
}
.hero-img {
	// background-attachment: fixed;
	background-size: cover;
	background-origin: 50% 50%;
	background-image: url("../assets/page_hero.jpg");
	// background-image: url("../assets/parallax_jewels/Nueva carpeta/jewel_composition.svg");

	height: 70vh;
}
.mint-section {
	height: 100vh;
	position: relative;
}
.starfield-background {
	position: absolute;
	width: 100%;
	height: 100vh;
	left: 0;
	top: 0;
	> * {
		position: absolute;
		top: 0;
		left: 0;
		background-size: contain;
		background-repeat: repeat;
		background-attachment: fixed;
		background-origin: center;
		width: 100%;
		height: 100%;
		mix-blend-mode: screen;
	}
	.parallax-0 {
		background-image: url("../assets/parallax_jewels/parallax_0.svg");
	}
	.parallax-1 {
		background-image: url("../assets/parallax_jewels/parallax_1.svg");
	}
	.parallax-2 {
		background-image: url("../assets/parallax_jewels/parallax_2.svg");
	}
	.parallax-3 {
		background-image: url("../assets/parallax_jewels/parallax_3.svg");
	}
	.parallax-background {
		background-size: cover;
		background-image: url("../assets/parallax_jewels/parallax_background.svg");
	}
}
.description-section {
	width: 100%;
}
</style>