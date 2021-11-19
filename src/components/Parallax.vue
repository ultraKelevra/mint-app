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
		<div class="minting-text-top">
			<h2>Join The Kidz!</h2>
			<h3>Join while you can!</h3>
			<p></p>
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

			this.offset_0 = 0.15 * percent;
			this.offset_1 = 0.2 * percent;
			this.offset_2 = 0.75 * percent;
			this.offset_3 = 1.25 * percent;
			console.log(percent);
			if (percent < 0) percent = 0;
			percent /= 100;
			if (percent > 1) percent = 1;
			this.black = percent;
		},
	},
	mounted() {
		window.addEventListener("scroll", this.setParallax);
		this.setParallax();
	},
};
</script>

<style lang="scss" scoped>
.black-cover {
	position: absolute;
	width: 100%;
	height: 100%;
	background: black;
}
.minting-section {
	position: relative;
	height: 70vh;
	overflow: hidden;
	background-attachment: fixed;
	background-color: rgb(41, 255, 21);
	background-position: center;
	background-size: cover;

	.parallax-background {
		background-size: cover;
		background-image: url("../assets/parallax_jewels/parallax_background.svg");
		width: 100%;
		height: 100%;
		position: absolute;
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