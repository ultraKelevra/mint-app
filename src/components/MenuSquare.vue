<template>
	<div class="menu-square">
		<slot></slot>
	</div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.menu-square {
	display: relative;
	background: red;
	border: solid 1px white;
	box-sizing: border-box;
	// width: 50vmin;
	// height: 50vmin;
}
</style>