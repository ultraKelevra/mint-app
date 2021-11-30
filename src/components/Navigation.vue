<template>
	<div class="navigation">
		<div class="container">
			<div
				class="nav-background"
				:style="{
					opacity: backgroundOpacity,
				}"
			></div>

			<div>
				<div class="hoodie-kidz-logo"></div>
				<div></div>
				<div class="nav-container">
					<div>Discord</div>
					<div>Tweeter</div>
					<div>About</div>
					<div>Roadmap</div>
					<div>Lore</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			backgroundOpacity: 0,
		};
	},
	methods: {
		setParallax() {
			var offsetTop = window.scrollY;
			var percent = offsetTop / 100;

			if (percent < 0) percent = 0;
			if (percent > 1) percent = 1;
			this.backgroundOpacity = percent;
		},
	},
	mounted() {
		window.addEventListener("scroll", this.setParallax);
		this.setParallax();
	},
	unmounted() {
		window.removeEventListener("scroll", this.setParallax);
	},
};
</script>

<style lang="scss">
.navigation {
	.nav-background {
		background: black;
		position: absolute !important;
		top: -20px;
		bottom: -20px;
		z-index: -1;
		width: 100vw !important;
		margin: 0 !important;
	}
	width: 100%;
	position: fixed;
	grid-template-columns: 1fr auto auto;
	z-index: 10000;
	color: white;
	.container {
		margin: 0 !important;
		padding: 0 !important;
		> * {
			margin: 0 !important;
			padding: 0 !important;
		}
	}
	.hoodie-kidz-logo {
		position: absolute;
		top: -5px;
		left: 0;
		width: 8vmin;
		bottom: -5px;
		background-repeat: no-repeat;
		background-size: contain;
		background-origin: 50% 50%;
		background-image: url("../assets/hoodie-kidz-logo.svg");
	}
	.container {
		> div {
			display: inline-flex;
			// top: 20px;
		}
	}
}
.nav-container {
	display: grid;
	grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
	font-weight: bold;
	text-align: center;
	grid-gap: 5px;
	align-content: center;
	margin-left: 15vh;
	font-size: 25px;
	height: 5vmin;
}

.small-display {
	.navigation {
		// .hoodie-kidz-logo {
		// }
	}
}
.small-horizontal-display {
	.navigation {
		margin-top: 15px;
		.hoodie-kidz-logo {
		}
		.nav-container {
			font-size: 18px;
		}
	}
}
.med-display {
	.navigation {
	}
}
.large-display {
	.navigation {
		margin-top: 15px;
		.hoodie-kidz-logo {
		}
	}
}
</style>