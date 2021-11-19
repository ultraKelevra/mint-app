<template>
	<!-- <div id="nav"> -->
	<!-- <router-link to="/"></router-link>| -->
	<!-- <router-link to="/about">About</router-link>| -->
	<!-- <router-link to="/grid">Grid</router-link> -->
	<!-- </div> -->
	<router-view />
</template>

<style lang="scss">
body {
	background: black;
}
* {
	margin: 0;
	padding: 0;
}
h1 {
	color: white;
}
h2 {
	colore: rgb(231, 231, 231);
}
h3 {
	colore: rgb(231, 231, 231);
}

p {
	colore: rgb(175, 175, 175);
}
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #ffffff;
}

#nav {
	padding: 30px;

	a {
		font-weight: bold;
		color: #35d0f6;

		&.router-link-exact-active {
			color: #35f09c;
		}
	}
}
</style>
