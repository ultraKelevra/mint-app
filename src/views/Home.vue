<template>
	<div
		class="home"
		id="home"
		:class="{
			horizontal: horizontal,
			vertical: !horizontal,
			'small-display': size == 0,
			'small-horizontal-display': size == 1,
			'med-display': size == 2,
			'large-display': size == 3,
		}"
	>
		<navigation></navigation>
		<hero></hero>
		<mint-area></mint-area>
		<kidz-band></kidz-band>

		<starmap id="starmap"></starmap>
		<f-a-q id="faq"></f-a-q>
		<cool-footer></cool-footer>
	</div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Hero from "../components/Hero.vue";
import MintArea from "../components/MintArea.vue";
import FAQ from "../components/FAQ.vue";

import KidzBand from "../components/KidzBand.vue";
import Starmap from "../components/Starmap.vue";
import CoolFooter from "../components/CoolFooter.vue";
import Navigation from "../components/Navigation.vue";
export default {
	name: "Home",
	data() {
		return {
			horizontal: false,
			size: 3,
		};
	},
	components: {
		Hero,
		MintArea,
		KidzBand,
		FAQ,

		Starmap,
		CoolFooter,
		Navigation,
	},
	methods: {
		resize() {
			var width = document.documentElement.clientWidth;
			var height = document.documentElement.clientHeight;

			this.horizontal = width > height;
			//large
			this.size = 3;
			//med
			if (width < 991) this.size = 2;
			//small
			if (width < 478) this.size = 0;
			if (this.horizontal && height < 478) {
				this.size = 1;
			}
		},
	},
	mounted() {
		window.addEventListener("resize", this.resize);
		this.resize();
	},
};
</script>
<style lang="scss">
.home {
	width: 100%;
}
</style>