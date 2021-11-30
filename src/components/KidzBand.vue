<template>
	<div class="kid-show"></div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.kid-show {
	position: relative;
	width: 100%;
	height: 50vw;
	background-image: url("../assets/kidz_big_band.jpg");
	background-size: cover;
}
@keyframes kid-square-sprite {
	100% {
		background-position-x: -400vw;
	}
}

.small-display {
	.kid-show {
		height: 100vw;
		background-position: left top;
		background-image: url("../assets/animation_frames.jpg");
		animation-name: kid-square-sprite;
		animation-duration: 4s;
		animation-iteration-count: infinite;
		animation-timing-function: steps(4);
	}
}
.med-display {
	.kid-show {
		height: 66.6vw;
	}
}
</style>