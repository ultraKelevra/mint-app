<template>
	<div class="minting-section">
		<div class="parallax-background">
			<div
				class="parallax-3"
				:style="{
					transform: 'translateY(' + offset_0 + '%)',
				}"
			></div>
			<div
				class="parallax-3-shine"
				:style="{
					transform: 'translateY(' + offset_0 + '%)',
				}"
			></div>
			<div
				class="parallax-2"
				:style="{ transform: 'translateY(' + offset_1 + '%)' }"
			></div>
			<div
				class="parallax-2-shine"
				:style="{ transform: 'translateY(' + offset_1 + '%)' }"
			></div>
			<div
				class="parallax-1"
				:style="{ transform: 'translateY(' + offset_2 + '%)' }"
			></div>
			<div
				class="parallax-1-shine"
				:style="{ transform: 'translateY(' + offset_2 + '%)' }"
			></div>
			<div
				class="parallax-0"
				:style="{ transform: 'translateY(' + offset_3 + '%)' }"
			></div>
			<div
				class="parallax-0-shine"
				:style="{ transform: 'translateY(' + offset_3 + '%)' }"
			></div>
		</div>
		<div class="black-cover" :style="{ opacity: black }"></div>
		<div class="container">
			<div class="minting-text-top">
				<div style="grid-area: a">
					<h2>Get a KID!</h2>
					<h3>Join while you can :)</h3>
				</div>
				<button style="grid-area: b">MINT</button>
				<p style="grid-area: c">
					By minting a Hoodie Kid you will become patreon of a
					passionate creative team ready to give it all in the future
					of the blockchain.
				</p>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			offset_0: 0,
			offset_1: 0,
			offset_2: 0,
			offset_3: 0,
			black: 0,
			initial_scroll: 0,
		};
	},
	methods: {
		setParallax() {
			var height = document.documentElement.clientHeight;
			var offsetTop = this.$el.getBoundingClientRect().top;
			var percent = (offsetTop / height) * 100;

			this.offset_0 = -0.75 * percent;
			this.offset_1 = -0.5 * percent;
			this.offset_2 = -0.3 * percent;
			this.offset_3 = -0.15 * percent;
			console.log(percent);
			if (percent < 0) percent = 0;
			percent /= 100;
			if (percent > 1) percent = 1;
			this.black = percent + 0.5 * percent + 0.25;
		},
	},
	mounted() {
		window.addEventListener("scroll", this.setParallax);
		this.setParallax();
		this.initial_scroll = this.$el.getBoundingClientRect().top;
	},
};
</script>

<style lang="scss">
.kidz-explanation {
	display: block;
	margin: 50px;
}
.small-display {
	.minting-section {
		.minting-text-top {
			grid-template-columns: 1fr;
			grid-template-rows: 15vh 15vh auto;
			grid-template-areas:
				" b "
				" a "
				" c ";
			h2 {
				text-align: left;
				font-weight: bolder;
				font-size: 30px;
				padding: 0 30px 0 30px;
			}
			h3 {
				text-align: left;
				font-size: 23px;
				padding: 0 30px 0 30px;
			}

			p {
				text-align: justify;
				font-size: calc(20px + 0.2vw);
				padding: 0px 30px 0 30px;
				line-height: calc(30px + 0.2vw);
			}
		}
	}
}
.small-horizontal-display {
	.minting-section {
		.minting-text-top {
			grid-template-columns: 1fr 1fr;
			grid-template-rows: 30vh auto;
			grid-template-areas:
				" a b "
				" c c ";
			h2 {
				text-align: left;
				font-weight: bolder;
				font-size: 40px;
				padding: 0;
			}
			h3 {
				text-align: left;
				font-size: 20px;
				padding: 0;
			}

			p {
				text-align: justify;
				font-size: calc(20px+0.5vw);
				padding: 0;
			}
			button {
				margin: 0 0 calc(2vw) 30px;
			}
		}
	}
}
.med-display {
	.minting-section {
		.minting-text-top {
			grid-template-columns: 1fr 1fr;
			grid-template-rows: 30vh auto;
			grid-template-areas:
				" a b "
				" c c ";
			h2 {
				text-align: left;
				font-weight: bolder;
				font-size: calc(40px + 1vh);
				padding: 50px 0 0 0;
			}
			h3 {
				text-align: left;
				font-size: calc(30px + 0.5vh);
				padding: 15px 0 0 0;
			}

			p {
				text-align: justify;
				font-size: calc(25px + 0.5vw);
				padding: 15px 0;
			}
			button {
				margin: 0 0 70px 30px;
				font-size: 50px;
			}
		}
	}
}
.large-display {
	.minting-section {
		.minting-text-top {
			grid-template-columns: 1fr 1fr;
			grid-template-rows: 30vh auto;
			grid-template-areas:
				" a b "
				" c c ";

			h2 {
				text-align: left;
				font-weight: bolder;
				font-size: 50px;
				padding: 60px 0 0;
			}
			h3 {
				text-align: left;
				font-size: 35px;
				padding: 10px 0 0 0;
				font-weight: normal;
			}

			p {
				// line-height: calc(50px + 0.5vw);
				text-align: justify;
				font-size: 30px;
				padding: 15px 0 0 0;
			}
			button {
				margin: 0 0 70px 50px;
				font-size: 60px;
			}
		}
	}
}

.black-cover {
	position: absolute;
	width: 100%;
	height: 100%;
	top: 0;
	background: black;
	// mask: url("../assets/scan-lines-black_white.png");
	// mask-size: 128px;
	// mask-size: calc((15vw + 15vh) / 2 + 64px);

	mask-repeat: repeat;
}

.minting-section {
	position: relative;
	background-attachment: fixed;
	background-color: rgb(0, 0, 0);
	background-position: center;
	background-size: cover;
	.parallax-background {
		overflow: hidden;
		background-size: cover;
		background-image: url("../assets/parallax_jewels/parallax_background.svg");
		width: 100%;
		height: 60vh;
		position: relative;
		background-attachment: fixed;
		> * {
			width: 100%;
			height: 100%;
			position: absolute;
			background-color: transparent;
			background-origin: center;
			background-repeat: no-repeat;
			background-size: contain;
		}
	}
	.minting-text-top {
		position: absolute;
		display: grid;
		top: 0;
		left: 0;
		height: 60vh;

		button {
			margin: 0 30px 0 30px;
			transform: translateY(-5vh);
			border-radius: 15px;
			border: solid 5px gold;
			background: black;
			color: gold;
			box-sizing: border-box;
			font-weight: bolder;
			font-size: xx-large;
			transition: border-width 0.25s, border-radius 0.25s, font-size 0.35s;
			&:hover {
				color: black;
				background: gold;
				border-color: black;
				border-width: 15px;
				border-radius: 25px;
			}
		}
		h2 {
			text-align: left;
			font-weight: bolder;
			font-size: 30px;
			padding: 0 30px 0 30px;
		}
		h3 {
			text-align: left;
			font-size: x-large;
			padding: 0 30px 0 30px;
		}
	}
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
.parallax-0-shine {
	mix-blend-mode: screen;
	background-image: url("../assets/parallax_jewels/parallax_0_shine.svg");
}
.parallax-1-shine {
	mix-blend-mode: screen;

	background-image: url("../assets/parallax_jewels/parallax_1_shine.svg");
}
.parallax-2-shine {
	mix-blend-mode: screen;

	background-image: url("../assets/parallax_jewels/parallax_2_shine.svg");
}
.parallax-3-shine {
	mix-blend-mode: screen;

	background-image: url("../assets/parallax_jewels/parallax_3_shine.svg");
}
</style>