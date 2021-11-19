<template>
	<div class="grid-container">
		<div
			class="base-grid"
			:class="[horizontal ? 'horizontal' : 'vertical']"
		>
			<menu-square class="a">KIDZ LOGO</menu-square>
			<menu-square class="b">MINT!</menu-square>
			<menu-square class="c">ROADMAP</menu-square>
			<menu-square class="f">HOW IS MADE</menu-square>
			<menu-square class="e">RARITY</menu-square>
			<menu-square class="d">LORE</menu-square>
		</div>
	</div>
</template>

<script>
import MenuSquare from "./MenuSquare.vue";
export default {
	data() {
		return {
			horizontal: false,
			minVal: 0,
		};
	},
	computed: {},
	components: {
		MenuSquare,
	},
	methods: {
		updateDimensions() {
			console.log("updatingDimensions");
			var width = document.documentElement.clientWidth;
			var height = document.documentElement.clientHeight;

			this.horizontal = width > height;
			this.minVal = Math.min(width, height) * 0.85;
		},
	},
	mounted() {
		window.addEventListener("resize", this.updateDimensions);
		this.updateDimensions();
	},
	unmounted() {
		window.removeEventListener("resize", this.updateDimensions);
	},
};
</script>

<style lang="scss">
.grid-container {
	position: absolute;
	top: 0;
	left: 0;
	bottom: 0;
	right: 0;
}

.base-grid {
	position: absolute;
	display: grid;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	text-align: start;
	width: 100%;
	height: 100%;

	&.horizontal {
		grid-template-areas:
			". . . . ."
			". a b c ."
			". d e f ."
			". . . . .";
		grid-template-columns: 10vmin repeat(3, 1fr) 10vmin;
		grid-template-rows: 10vmin repeat(2, 1fr) 10vmin;
	}

	&.vertical {
		grid-template-columns: repeat(2, 1fr);
		grid-template-rows: 15vmin repeat(3, 1fr) 15vmin;
		grid-template-areas:
			" . . "
			" a b "
			" c d "
			" e f "
			" . . ";
	}
}

.base-grid > * {
	position: relative;
}

.a {
	grid-area: a;
}

.b {
	grid-area: b;
}

.c {
	grid-area: c;
}

.d {
	grid-area: d;
}

.e {
	grid-area: e;
}

.f {
	grid-area: f;
}
</style>