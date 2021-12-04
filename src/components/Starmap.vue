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
				<div class="b empty"></div>
				<div class="c">
					<img
						ref="rocket"
						src="../assets/starmap/rocket_boy.png"
						alt=""
						class="rocket-figure"
					/>
					<img
						ref="stars_0"
						src="../assets/starmap/stars_0.svg"
						alt=""
						class="moon-figure"
					/>
					<img
						ref="moon"
						src="../assets/starmap/moon.svg"
						alt=""
						class="moon-figure"
					/>
				</div>
				<div class="d description">
					<h3>Minting is open</h3>
					<p>
						Lorem ipsum dolor sit amet, consectetur adipisicing
						elit, sed do eiusmod tempor incididunt ut labore et
						dolore magna aliqua. Ut enim ad minim veniam.
					</p>
				</div>
				<div class="a empty"></div>
				<div class="b">
					<span class="purple important-data"> 50% minting </span>
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
				<div class="d empty"></div>
				<div class="a"><span class="date salmon">2022/MAR </span></div>
				<div class="b empty"></div>
				<div class="c empty"></div>
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
				<div class="a empty"></div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			black: 0,
		};
	},
	methods: {
		setParallax() {
			var height = window.screen.availHeight;
			var offsetTop = this.$el.getBoundingClientRect().top;
			var percent = 1 - (height - offsetTop) / height + 1;
			this.black = percent;
		},
	},
	components: {},
	mounted() {
		var self = this;
		var lerp = function (a, b, t) {
			return a + (b - a) * t;
		};
		var invLerp = function (a, b, c) {
			return (c - a) / (b - a);
		};
		var setParallaxFrame = function () {
			window.requestAnimationFrame(setParallaxFrame);

			var height = window.screen.availHeight;
			var parallaxPerElement = function (elem, start, end) {
				var pbbox = elem.parentNode.getBoundingClientRect();

				var bbox = elem.getBoundingClientRect();
				var scroll = window.scrollY;

				var top = pbbox.top + elem.offsetTop;
				var bottom = top + bbox.height + scroll;
				var parallaxTop = top + start * height;
				var parallaxBottom = bottom + end * height;

				var t = invLerp(
					parallaxTop,
					parallaxBottom,
					document.documentElement.scrollTop
				);

				var visible = t >= 0 && t <= 1;
				if (!visible) return;

				elem.style.transform =
					"translateY(" +
					Math.round(lerp(start, end, t) * height) +
					"px)";
			};
			parallaxPerElement(self.$refs.rocket, 0.3, -0.3);
			parallaxPerElement(self.$refs.moon, -0.5, 0.5);
			parallaxPerElement(self.$refs.stars_0, -1.5, 1.5);
		};
		window.requestAnimationFrame(setParallaxFrame);
		window.addEventListener("scroll", this.setParallax);
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
	.starmap {
		overflow: hidden;
		.starmap-grid {
			grid-template-columns: 0;
			grid-template-areas: "t";
			grid-template-columns: 100vw;
			grid-template-rows: 25vh 25vh 50vh 25vh 50vh 25vh 50vh;
			.date {
				font-size: 50px;
			}
			.empty {
				display: none;
			}
			.c,
			.d {
				padding: 30px 0 20px 0;
			}
			.a {
				transform: translate(-30px, 30px);
			}
			.b {
				transform: translate(30px, 30px);
			}
		}
	}
}
.small-horizontal-display {
	.starmap {
		.starmap-grid {
			grid-template-columns: 1fr 1fr;
		}
	}
}
.med-display {
	.starmap {
		.starmap-grid {
			grid-template-columns: calc(50vw - 60px) calc(50vw - 60px);
			.a,
			.b,
			.c,
			.d {
				margin: 0 -60px;
			}
		}
	}
}

.large-display {
	.rocket-figure {
		position: absolute;
		right: 0;
		top: 15vh;
		width: 65vw;
		z-index: 1000;
	}
	.moon-figure {
		position: absolute;
		top: -25vh;
		width: 100vw;
		right: -50vw;
		filter: drop-shadow(0 0 25px yellow) saturate(0.5);
		// transition: 1s;
	}

	.starmap {
		.starmap-grid {
			grid-template-columns: 400px 400px;
			grid-template-areas: "t t";
			grid-template-rows: 75vh 25vh 60vh 25vh 60vh 25vh 100vh;
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
				align-items: stretch;
			}
			.a {
				transform: translate(100px, 70px);
				font-weight: bold;
				z-index: 5;
			}
			.b {
				transform: translate(-100px, 70px);
				font-weight: bold !important;
			}
			.c {
				padding: 50px 20px;
				h3 {
					text-align: rigth;
				}
			}
			.d {
				padding: 50px 20px;
			}
		}
	}
}
.starmap {
	position: relative;
	background: url("../assets/starmap_bg.svg");
	background-size: cover;
	background-attachment: fixed;
	overflow: hidden;
	.starmap-grid {
		display: grid;

		.t {
			grid-area: t;
			display: flex;
			justify-content: flex-end;
			align-items: stretch;
			flex-direction: column;
		}
		.a {
			justify-content: flex-end;
			display: flex;
			align-items: flex-end;
			font-weight: bold;
			z-index: 5;
		}
		.b {
			justify-content: flex-end;
			display: flex;
			align-items: flex-start;
			font-weight: bold !important;
			z-index: 5;
			flex-direction: column;
		}
		.c {
			position: relative;
			display: flex;
			flex-direction: column;
			justify-content: flex-start;
		}
		.d {
			position: relative;
			display: flex;
			flex-direction: column;
			justify-content: flex-start;
		}
	}
}
</style>