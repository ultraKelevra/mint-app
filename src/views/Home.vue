<template>
	<div
		class="home"
		:class="{
			horizontal: horizontal,
			vertical: !horizontal,
			'small-display': size == 0,
			'small-horizontal-display': size == 1,
			'med-display': size == 2,
			'large-display': size == 3,
		}"
	>
		<hero></hero>
		<mint-button></mint-button>
		<div style="height: 100vh; background: black"></div>
	</div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Hero from "../components/Hero.vue";
import MintButton from "../components/MintButton.vue";
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
		MintButton,
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
.container {
	position: absolute;
	width: 100%;
	top: 0;
	margin: auto;
	justify-items: center;
}
.med-display {
	.container {
		> * {
			margin-left: 50px;
			margin-right: 50px;
		}
	}
}

.small-display {
	.container {
		> * {
			margin-left: 0;
			margin-right: 0;
		}
	}
}
.small-horizontal-display {
	.container {
		> * {
			margin-left: 80px;
			margin-right: 80px;
		}
	}
}
.large-display {
	.container {
		> * {
			display: inline-grid;
			width: 800px;
			position: relative;
		}
	}
}
.home {
	width: 100%;
}
</style>