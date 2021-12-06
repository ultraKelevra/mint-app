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
				<div class="a"><span class="date pink">2022/JAN</span></div>
				<div class="b empty"></div>
				<div class="c">
					<img
						ref="rocket"
						src="../assets/starmap/rocket_boy.png"
						alt=""
						class="rocket-figure"
					/>
					<img
						ref="stars"
						src="../assets/starmap/stars.svg"
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
					<span class="date purple">2022/FEB </span>
				</div>
				<div class="c description">
					<h3>Move to an office</h3>
					<p>
						Lorem ipsum dolor sit amet, consectetur adipisicing
						elit, sed do eiusmod tempor incididunt ut labore et
						dolore magna aliqua. Ut enim ad minim veniam.
					</p>
				</div>
				<div class="d">
					<img
						ref="computer"
						class="computer"
						src="../assets/starmap/computer.png"
						alt=""
					/>
					<img
						ref="floppy_0"
						class="floppy-0"
						src="../assets/starmap/floppy_0.png"
						alt=""
					/>
					<img
						ref="floppy_1"
						class="floppy-1"
						src="../assets/starmap/floppy_1.png"
						alt=""
					/>
				</div>
				<div class="a"><span class="date salmon">2022/MAY </span></div>
				<div class="b empty"></div>
				<div class="c">
					<img
						ref="gamekid"
						class="gamekid"
						src="../assets/starmap/gamekid.png"
						alt=""
					/>
					<img
						ref="sword"
						class="sword"
						src="../assets/starmap/sword.png"
						alt=""
					/>
					<img
						ref="crown_1"
						class="crown-1"
						src="../assets/starmap/crown_1.png"
						alt=""
					/>

					<img
						ref="crown_0"
						class="crown-0"
						src="../assets/starmap/crown_0.png"
						alt=""
					/>

					<img
						ref="medallion"
						class="medallion"
						src="../assets/starmap/medallion.png"
						alt=""
					/>
				</div>
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
				<div class="b">
					<span class="purple important-data"> 100% minting </span>
					<span class="date purple">2022/XX </span>
				</div>
				<div class="c description">
					<h3>We'll see...</h3>
					<p>
						Once reached this point, our main objective will be to
						preserve the value our product will have.
						<span class="important"
							>Keeping the game exciting and updated will be
							priority</span
						>.<br /><br />The
						<span class="gold">patreons</span> will then vote for
						what will <span class="important">The Team</span> work
						on next.<br /><br />
						It's hard to plan so far ahead. Jump in and let's see
						what cool, exciting and weird stuff we end up building
						:)
					</p>
				</div>
				<div class="d"></div>
			</div>
			<img
				class="starmap-clouds"
				src="../assets/starmap/clouds.svg"
				alt=""
			/>
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
			parallaxPerElement(self.$refs.stars, -1, 1);
			parallaxPerElement(self.$refs.computer, 0.3, -0.1);
			parallaxPerElement(self.$refs.floppy_0, 0.7, -0.1);
			parallaxPerElement(self.$refs.floppy_1, 0.5, -0.75);

			//3rd
			parallaxPerElement(self.$refs.sword, 0.5, -0.2);
			parallaxPerElement(self.$refs.crown_0, 0.9, -0.3);
			parallaxPerElement(self.$refs.crown_1, 1, -0.2);
			parallaxPerElement(self.$refs.gamekid, 0.5, -0.2);
			parallaxPerElement(self.$refs.medallion, 1.3, -0.35);
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
	}
	.computer {
		position: absolute;
		bottom: -15vh;
		width: 25vw;
		left: -7vh;
	}
	.floppy-0 {
		position: absolute;
		bottom: 25vh;
		width: 10vw;
		left: 0;
	}
	.floppy-1 {
		position: absolute;
		bottom: -25vh;
		width: 18vw;
		left: 20vh;
		filter: blur(3px);
		z-index: 5;
	}

	.medallion {
		position: absolute;
		right: 15vw;
		top: 35vh;
		width: 15vw;
		z-index: 1000;
	}
	.crown-0 {
		position: absolute;
		right: 0;
		top: 45vh;
		width: 15vw;
		z-index: 1000;
	}
	.crown-1 {
		position: absolute;
		right: 5vw;
		top: 75vh;
		width: 10vw;
		z-index: 1000;
	}
	.gamekid {
		position: absolute;
		right: 12vw;
		top: 65vh;
		width: 17vw;
		z-index: 1000;
	}

	.sword {
		position: absolute;
		right: -45px;
		top: 10vh;
		width: 30vw;
		z-index: 1000;
	}

	.starmap {
		.starmap-clouds {
			position: absolute;
			width: 100vw;
			left: 0;
			bottom: -2px;
		}
		.container {
			padding-bottom: 50vh;
		}
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