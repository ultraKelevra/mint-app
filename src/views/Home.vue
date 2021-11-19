<template>
	<div class="home">
		<hero></hero>
	</div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Hero from "../components/Hero.vue";

export default {
	name: "Home",
	components: {
		// HelloWorld
		Hero,
	},
};
</script>
<style lang="scss">
.home {
	width: 100%;
}
</style>