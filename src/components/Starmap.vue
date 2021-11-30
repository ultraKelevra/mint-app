<template>
	<div class="starmap">
		<div
			class="black-cover"
			:style="{ opacity: black }"
			v-show="black > 0"
		></div>
		<!-- <parallax-background></parallax-background> -->
		<div class="container">
			<div class="starmap-grid">
				<div class="t">
					<h2>STARMAP</h2>
				</div>
				<div class="a"><span class="date pink">DEC/25</span></div>
				<div class="b"></div>
				<div class="c"></div>
				<div class="d description">
					<h3>Minting is open</h3>
					<p>
						Lorem ipsum dolor sit amet, consectetur adipisicing
						elit, sed do eiusmod tempor incididunt ut labore et
						dolore magna aliqua. Ut enim ad minim veniam.
					</p>
				</div>
				<div class="a"></div>
				<div class="b">
					<span class="purple important-data" style="font-size: 50px">
						50% minting
					</span>
					<span class="date purple">2022/JAN </span>
				</div>
				<div class="c description">
					<h3>Move to an office</h3>
					<p>
						Lorem ipsum dolor sit amet, consectetur adipisicing
						elit, sed do eiusmod tempor incididunt ut labore et
						dolore magna aliqua. Ut enim ad minim veniam.
					</p>
				</div>
				<div class="d"></div>
				<div class="a"><span class="date salmon">2022/MAR </span></div>
				<div class="b"></div>
				<div class="c"></div>
				<div class="d important-description starchild">
					<h3>Release Beta of "Staff of Mana" (Play to earn game)</h3>
					<p>
						Lorem ipsum dolor sit amet, consectetur adipisicing
						elit, sed do eiusmod tempor incididunt ut labore et
						dolore magna aliqua. Ut enim ad minim veniam. Lorem
						ipsum dolor sit amet, consectetur adipisicing elit, sed
						do eiusmod tempor incididunt ut labore et dolore magna
						aliqua. Ut enim ad minim veniam.
					</p>
				</div>
				<div class="a"></div>
			</div>
		</div>
	</div>
</template>

<script>
// import ParallaxBackground from "./ParallaxBackground.vue";
export default {
	data() {
		return {
			black: 0,
		};
	},
	methods: {
		setParallax() {
			var height = document.documentElement.clientHeight;
			var offsetTop = this.$el.getBoundingClientRect().top;
			var percent = (offsetTop / height) * 100;

			// this.offset_0 = 2 * percent;
			// this.offset_1 = -0.5 * percent;
			// this.offset_2 = -0.3 * percent;
			// this.offset_3 = -0.15 * percent;
			// console.log(percent + percent);

			if (percent < 0) percent = 0;
			percent /= 100;
			if (percent > 1) percent = 1;
			this.black = percent + percent * 2;
		},
	},
	components: {
		// ParallaxBackground,
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
.black-cover {
	position: absolute;
	width: 100%;
	height: 100%;
	top: 0;
	background: black;
	mask-repeat: repeat;
}
.starchild {
	background-image: url("../assets/treehouse-background/bg_0.svg");
	background-size: cover;
	background-attachment: fixed;
}
.date {
	font-size: 80px;
	background: #ffdd7d;
	padding: 0 20px;
}
.important-data {
	background: #ffdd7d;
	padding: 0 20px;
}
.important h3 {
	font-weight: bold;
}
.purple {
	color: #704fbf;
}
.salmon {
	color: #fa8085;
}
.pink {
	color: #eb52b3;
}

.description {
	background-color: rgb(36, 36, 36);
}

.important-description {
	background-color: rgb(238, 190, 57);
	h3 {
		color: rgb(30, 30, 30);
	}
	p {
		color: rgb(30, 30, 30);
	}
}
.small-display {
	.starmap-grid {
		grid-template-columns: 1fr;
	}
}
.small-horizontal-display {
	.starmap-grid {
		grid-template-columns: 1fr 1fr;
	}
}
.med-display {
	.starmap {
		.starmap-grid {
			// grid-template-columns: 400px 400px;
			grid-template-columns: calc(50vw - 50px) calc(50vw - 50px);
			.a,
			.b,
			.c,
			.d {
				margin: 0 -50px;
			}
		}
	}
}

.large-display {
	.starmap {
		.starmap-grid {
			grid-template-columns: 400px 400px;
		}
	}
}
.starmap {
	position: relative;
	background: url("../assets/starmap_bg.svg");
	background-size: cover;
	background-attachment: fixed;
	background-position-y: 10vh;
	.starmap-grid {
		grid-template-areas: "t t";
		display: grid;
		grid-template-columns: 200px 200px;
		grid-template-rows: 30vh 25vh 60vh 25vh 60vh 25vh 100vh;
		h2 {
			margin: 0;
			padding: 0;
		}
		> * {
			position: relative;
			display: flex;
			flex-direction: column;
		}
		.t {
			grid-area: t;
			display: flex;
			justify-content: flex-end;
			align-items: stretch;
			flex-direction: column;
		}
		.a {
			justify-content: flex-end;
			/* background: red; */
			display: flex;
			align-items: flex-end;
			transform: translate(100px, 70px);
			font-weight: bold;
			z-index: 5;
		}
		.b {
			justify-content: flex-end;
			display: flex;
			align-items: flex-start;
			transform: translate(-100px, 70px);
			font-weight: bold !important;
			z-index: 5;
			color: #704fbf;
		}
		.c {
			padding: 50px 20px;
			position: relative;
			display: flex;
			flex-direction: column;
			justify-content: flex-start;
			h3 {
				text-align: rigth;
			}
		}
		.d {
			padding: 50px 20px;
			position: relative;
			display: flex;
			flex-direction: column;
			justify-content: flex-start;
		}
	}
}
</style>