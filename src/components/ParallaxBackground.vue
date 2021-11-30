<template>
	<div class="starmap-parallax-background"></div>
	<div class="black-cover" :style="{ opacity: black }"></div>
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
			var offsetTop = this.$el.parentNode.getBoundingClientRect().top;
			var percent = (offsetTop / height) * 100;

			this.offset_0 = 2 * percent;
			this.offset_1 = -0.5 * percent;
			this.offset_2 = -0.3 * percent;
			this.offset_3 = -0.15 * percent;
			if (percent < 0) percent = 0;
			percent /= 100;
			if (percent > 1) percent = 1;
			this.black = percent + percent;
		},
	},
	mounted() {
		window.addEventListener("scroll", this.setParallax);
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
.starmap-parallax-background {
	position: absolute;
	width: 100%;
	height: 100%;
	background: url("../assets/starmap_bg.svg");
	background-size: cover;
	position: absolute;
	background-attachment: fixed;

	> * {
		background-size: cover;
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
	}
}
</style>