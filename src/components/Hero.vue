<template>
	<div class="hero">
		<parallax-hero></parallax-hero>
		<div class="container">
			<div class="hero-elements">
				<div class="hoodie-kidz-text"></div>
			</div>
		</div>
	</div>
</template>

<script>
import ParallaxHero from "./ParallaxHero.vue";
export default {
	components: {
		ParallaxHero,
	},
};
</script>

<style lang="scss">
.hero {
	width: 100%;
	// height: 100vh;
	position: relative;
	.hero-elements {
		position: relative;
		height: 100%;
		width: 100%;
		.hoodie-kidz-text {
			position: absolute;
		}
	}
	.container {
		position: absolute;
	}
}
.small-display {
	.hero {
		height: 70vh;
	}
	.hero-elements {
		margin: 0 30px;
		width: calc(100% - 60px);
	}
}

.small-horizontal-display {
	.hero {
		height: 80vh;
	}
	.hero-elements {
		// padding: 0 30px;
	}
}
.med-display {
	.hero {
		height: 70vh;
	}
	.hero-elements {
		// margin: 0 80px;
		width: calc(100% - 160px);
	}
}
.large-display {
	.hero {
		height: 80vh;
	}
	.hero-elements {
		.hoodie-kidz-text {
			width: 800px;
			left: 50%;
			transform: translateX(-50%);
		}
		// padding: 0 30px;
		// height: 80vh;
	}
}

.hoodie-kidz-text {
	background-size: contain;
	background-position: center;
	background-image: url("../assets/hoodie-kidz-text.svg");
	background-repeat: no-repeat;
	// filter: drop-shadow(2px 2px 5px rgba(255, 0, 0, 0.322))
	// 	drop-shadow(-2px -2px 5px rgba(0, 0, 255, 0.404));
	// box-shadow:1px 1px 1px  orangered;
	filter: drop-shadow(5px 5px 0px rgba(0, 0, 0, 0.4));
	transition: 0.15s;
	mask-size: 128px;
	mask-repeat: repeat;
	position: relative;
	top: 25vh;
	left: 0;
	width: 100%;
	height: 30vh;
	// mix-blend-mode: screen;
	transition: 0.15s;
}
</style>