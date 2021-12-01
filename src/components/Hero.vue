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
		padding: 0;
	}
}
.small-display {
	.hero {
		height: 70vh;
	}
	.hero-elements {
		margin: 0 30px;
		width: calc(100% - 60px);
		.hoodie-kidz-text {
			height: 30vh;
			top: 35vh;
		}
	}
}

.small-horizontal-display {
	.hero {
		height: 80vh;
	}
	.hero-elements {
		.hoodie-kidz-text {
			top: 37.5vh;
			height: 25vh;
		}
	}
}
.med-display {
	.hero {
		height: 70vh;
	}
	.hero-elements {
		.hoodie-kidz-text {
			top: 30vh;
			height: 25vh;
		}
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
			top: 35vh;
			height: 30vh;
		}
	}
}
.hero {
	.hoodie-kidz-text {
		background-size: contain;
		background-position: center;
		background-image: url("../assets/hoodie-kidz-text.svg");
		background-repeat: no-repeat;
		filter: drop-shadow(5px 5px 0px rgba(0, 0, 0, 0.4));
		position: relative;
		width: 100%;
	}
}
</style>