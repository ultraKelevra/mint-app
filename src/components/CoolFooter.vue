<template>
	<div class="footer">
		<div class="container">
			<div class="nav-container">
				<div class="discord"></div>
				<div class="twitter"></div>
				<div class="inner-navigation">
					<a href="#mint" style="font-weight: bold; color: gold"
						>MINT</a
					>
					<a href="#about">About</a>
					<a href="#starmap">Starmap</a>
					<a href="#faq">FAQ</a>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.footer {
	background: url("../assets/starmap/starmap_tall_bg.svg");
	background-size: cover;
	position: relative;

	a {
		text-decoration: none;
		color: white;
	}
	.container {
		height: 100%;
		padding: 0 !important;
		display: flex;
		flex-direction: row;
		align-content: flex-end;
		justify-content: center;
		align-items: center;

		> * {
			height: 100%;
			display: flex;
			flex-direction: row;
			align-content: flex-end;
			justify-content: center;
			padding: 40px 0 60px 0;
		}
		.inner-navigation {
			display: flex;
			flex-direction: column;
			align-items: flex-start;
			justify-content: space-evenly;
			height: 100%;
			padding-left: 15px;
			grid-gap: 15px;
		}
	}

	.hoodie-kidz-logo {
		position: absolute;
		top: 0px;
		left: 0;
		width: 10vmin;
		bottom: 0px;
		background-repeat: no-repeat;
		background-size: contain;
		background-position: center;
		background-image: url("../assets/hoodie-kidz-logo.svg");
	}
}
.small-display {
	.footer {
		.inner-navigation {
			font-size: 5vw;
		}
	}
}
</style>