<template>
	<router-view />
</template>

<style lang="scss">
h2 {
	text-align: left;
	font-weight: bolder;
	font-size: calc(5vh);
	padding: 30px 30px 0 30px;
}
h3 {
	text-align: left;
	font-size: x-large;
	padding: 0 0 0 30px;
	// white-space: nowrap;
}
p {
	text-align: justify;
	font-size: 20px;
	padding: 40px 30px 0 30px;
	font-weight: lighter;
}

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
	font-family: Yu Gothic UI;
	// font-family: Avenir, Helvetica, Arial, sans-serif;
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
