<template>
	<div class="hero">
		<div class="container">
			<div class="hero-elements">
				<div class="hoodie-kidz-logo"></div>
				<!-- <div class="scan-lines"></div>
				<div class="scan-lines-dark"></div> -->
				<div class="hoodie-kidz-text"></div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	components: {},
};
</script>

<style lang="scss">
.hero {
	width: 100%;
	height: 70vh;
	background-position: center;
	background-size: cover;
	background-image: url(/img/page_hero.b1049f24.jpg);
	position: relative;
	.hero-elements {
		position: relative;
		height: 100%;
	}
}
.small-display {
	.hero-elements {
		padding: 0 30px;
	}
}

.small-horizontal-display {
	.hero-elements {
		// padding: 0 30px;
	}
}
.med-display {
	.hero-elements {
		// padding: 0 30px;
	}
}
.large-display {
	.hero-elements {
		// padding: 0 30px;
	}
}
.hoodie-kidz-logo {
	position: absolute;
	top: 0;
	left: 0;
	width: 65px;
	height: 64px;
	background-size: contain;
	background-origin: 50% 50%;
	background-image: url("../assets/hoodie-kidz-logo.svg");
	mask: url("../assets/scan-lines-black_white.png");
	// mask-size: 128px;
	mask-size: 128px;

	// mask-size: calc((15vw + 15vh) / 2 + 64px);

	mask-repeat: repeat;
	filter: drop-shadow(2px 2px 1px red) drop-shadow(-2px -2px 1px blue)
		blur(1px);
}
.hoodie-kidz-text {
	background-size: contain;
	background-position: center;
	background-image: url("../assets/hoodie-kidz-text.svg");
	background-repeat: no-repeat;
	filter: drop-shadow(2px 2px 1px red) drop-shadow(-2px -2px 1px blue)
		blur(1px);
	transition: 0.15s;
	mask: url("../assets/scan-lines-black_white.png");
	// mask-size: calc((15vw + 15vh) / 2 + 64px);
	mask-size: 128px;
	mask-repeat: repeat;
	position: relative;
	top: 15vh;
	left: 0;
	width: 100%;
	height: 40vh;
	filter: drop-shadow(2px 2px 1px red) drop-shadow(-2px -2px 1px blue)
		blur(1px);
	mix-blend-mode: screen;
	transition: 0.15s;
}
</style>