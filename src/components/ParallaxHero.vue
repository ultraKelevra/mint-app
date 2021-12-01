<template>
	<div class="parallax-background">
		<img
			ref="parallax_1"
			class="parallax-1"
			src="../assets/treehouse-background/bg_1.svg"
		/>
		<img
			ref="parallax_2"
			class="parallax-2"
			src="../assets/treehouse-background/bg_2.png"
		/>
		<img
			ref="parallax_3"
			class="parallax-3"
			src="../assets/treehouse-background/bg_3.png"
		/>
		<img
			class="parallax-foreground"
			src="../assets/treehouse-background/parallax-foreground.svg"
		/>
	</div>
</template>

<script>
export default {
	data() {
		return {};
	},
	methods: {},
	mounted() {
		var self = this;
		var setParallaxFrame = function () {
			window.requestAnimationFrame(setParallaxFrame);

			var height = document.documentElement.clientHeight;

			var offsetTop = self.$el.parentNode.getBoundingClientRect().top;
			var visible = offsetTop / height > -1;
			if (!visible) return;
			var percent = (offsetTop / height) * 100;

			if (!visible) return;

			self.$refs.parallax_1.style.transform =
				"translateY(" + -0.75 * percent + "%)";
			self.$refs.parallax_2.style.transform =
				"translateY(" + -0.6 * percent + "%)";
			self.$refs.parallax_3.style.transform =
				"translateY(" + -0.4 * percent + "%)";
		};
		window.requestAnimationFrame(setParallaxFrame);
	},
	unmounted() {},
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

	> * {
		position: absolute;
		background-color: transparent;
		background-position: left bottom;
		background-repeat: no-repeat;
		background-size: cover;
	}
	.parallax-1 {
		right: 0;
		left: 0;
		bottom: 0;
	}

	.parallax-2 {
		left: 0;
		height: 100%;
		bottom: 0;
	}
	.parallax-3 {
		top: 0;
		right: 0;
		height: 100%;
	}
	.parallax-foreground {
		bottom: 0;
		left: 0;
		width: 100%;
	}
}
</style>