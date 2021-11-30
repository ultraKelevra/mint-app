<template>
	<div class="parallax-background">
		<div
			class="parallax-1"
			:style="{ transform: 'translateY(' + offset_1 + '%)' }"
		></div>
		<div
			class="parallax-2"
			:style="{ transform: 'translateY(' + offset_2 + '%)' }"
		></div>
		<div
			class="parallax-3"
			:style="{ transform: 'translateY(' + offset_3 + '%)' }"
		></div>
		<div
			class="parallax-4"
			:style="{ transform: 'translateY(' + offset_3 + '%)' }"
		></div>
		<div
			class="parallax-5"
			:style="{ transform: 'translateY(' + offset_4 + '%)' }"
		></div>
		<div
			class="parallax-6"
			:style="{ transform: 'translateY(' + offset_4 + '%)' }"
		></div>
		<div class="parallax-foreground"></div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			offset_1: 0,
			offset_2: 0,
			offset_3: 0,
			offset_4: 0,

			initial_scroll: 0,
		};
	},
	methods: {
		setParallax() {
			var height = document.documentElement.clientHeight;
			var offsetTop = this.$el.parentNode.getBoundingClientRect().top;
			var percent = (offsetTop / height) * 100;

			this.offset_1 = -0.75 * percent;
			this.offset_2 = -0.6 * percent;
			this.offset_3 = -0.4 * percent;
			this.offset_4 = -0.3 * percent;
			this.offset_5 = -1 * percent;

			// console.log(percent);
			if (percent < 0) percent = 0;
			percent /= 100;
			if (percent > 1) percent = 1;
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
.vertical {
	.parallax-background {
		background-size: auto 100%;
		background-attachment: fixed;
	}
}
.horizontal {
	.parallax-background {
		// background-position-y: -25vh;
	}
}
.parallax-background {
	overflow: hidden;
	background-size: cover;
	background-image: url("../assets/treehouse-background/bg_0.svg");
	background-attachment: fixed;
	width: 100%;
	height: 100%;
	position: relative;
	background-position: bottom;

	// background-attachment: fixed;
	> * {
		width: 100%;
		height: 100%;
		position: absolute;
		background-color: transparent;
		background-position: left bottom;
		background-repeat: no-repeat;
		background-size: cover;
	}
	.parallax-0 {
		background-attachment: fixed;
		background-image: url("../assets/treehouse-background/bg_0.svg");
	}
	.parallax-1 {
		background-position: right bottom;

		background-image: url("../assets/treehouse-background/bg_1.svg");
	}
	.parallax-2 {
		background-position: right bottom;

		background-image: url("../assets/treehouse-background/bg_2.svg");
	}
	.parallax-3 {
		background-image: url("../assets/treehouse-background/bg_3.png");
	}
	.parallax-4 {
		background-position: left bottom;
		background-image: url("../assets/treehouse-background/bg_4.svg");
		mix-blend-mode: screen;
		opacity: 0.5;
	}
	.parallax-5 {
		background-position: left top;
		background-image: url("../assets/treehouse-background/bg_5.svg");
		mix-blend-mode: screen;
	}
	.parallax-6 {
		background-position: left top;
		background-image: url("../assets/treehouse-background/bg_6.png");
	}
	.parallax-foreground {
		background-image: url("../assets/treehouse-background/parallax-foreground.svg");
	}
}
</style>