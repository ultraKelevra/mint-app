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
				<div class="c empty"></div>
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
// import ParallaxBackground from "./ParallaxBackground.vue";
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
	.starmap {
		.starmap-grid {
			grid-template-columns: 400px 400px;
			grid-template-areas: "t t";
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
	// background-position-y: calc(5vh + 33px);
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