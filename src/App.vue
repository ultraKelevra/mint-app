<template>
	<router-view />
</template>

<style lang="scss">
section {
	position: relative;
	display: flex;
	align-items: center;
	box-sizing: border-box;
}
.container {
	position: relative;
	width: 100%;
	display: flex;
	top: 0;
	flex-direction: column;
	justify-items: center;
	align-items: center;
	justify-content: center;
	height: 100%;
	padding: 50px 0;
	> * {
		position: relative;
		display: flex;
		flex-direction: column;
	}
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
.orange {
	color: rgb(255, 127, 81);
	font-weight: normal;
	// filter: drop-shadow(1px 1px 0px red) drop-shadow(-1px -1px 0px blue);
}
.epic {
	color: violet;
	font-weight: normal;
	// filter: drop-shadow(1px 1px 3px red) drop-shadow(-1px -1px 3px blue);
}
.gold {
	color: gold;
	font-weight: normal;
	// filter: drop-shadow(1px 1px 3px red) drop-shadow(-1px -1px 3px blue);
}
.important {
	color: white;
	font-weight: normal;
	// filter: drop-shadow(1px 1px 3px red) drop-shadow(-1px -1px 3px blue);
}
.date {
	background: #ffdd7d;
	padding: 0 20px;
}
.important-data {
	background: #ffdd7d;
	padding: 0 20px;
	font-size: 50px;
}
.important h3 {
	font-weight: bold;
}
.purple {
	color: #704fbf;
}
.salmon {
	color: #fa8085;
}
.pink {
	color: #eb52b3;
}

.description {
	background-color: rgb(36, 36, 36);
}
.large-display {
	.date {
		font-size: 80px;
	}
	h2 {
		text-align: left;
		font-weight: bolder;
		font-size: 100px;
		padding: 60px 0 0;
	}
	h3 {
		text-align: left;
		font-size: 35px;
		padding: 30px 0 0 0;
		font-weight: normal;
	}

	p {
		// line-height: calc(50px + 0.5vw);
		text-align: justify;
		font-size: 30px;
		padding: 10px 0;
	}
}
.med-display {
	.date {
		font-size: 80px;
	}
	h2 {
		text-align: left;
		font-weight: bolder;
		font-size: 80px;
		padding: 50px 0 0 0;
	}
	h3 {
		text-align: left;
		font-size: calc(30px + 0.5vh);
		padding: 15px 0 0 0;
	}

	p {
		text-align: justify;
		font-size: calc(25px + 0.5vw);
		padding: 10px 0;
	}
}
.small-horizontal-display {
	.date {
		font-size: 70px;
	}
	h2 {
		text-align: left;
		font-weight: bolder;
		font-size: 70px;
		padding: 0;
	}
	h3 {
		text-align: left;
		font-size: 20px;
		padding: 20px 0 5px 0;
	}

	p {
		text-align: justify;
		font-size: calc(20px+0.5vw);
		padding: 10px 0;
	}
}
.small-display {
	.important-data {
		font-size: 30px;
	}
	.date {
		font-size: 50px;
	}
	h2 {
		text-align: left;
		font-weight: bolder;
		font-size: 50px;
		padding: 0 30px 0 30px;
	}
	h3 {
		text-align: left;
		font-size: 25px;
		padding: 30px 30px 0 30px;
	}

	p {
		text-align: justify;
		font-size: calc(20px + 0.2vw);
		padding: 10px 30px;
		line-height: calc(30px + 0.2vw);
	}
}
h2 {
	text-align: left;
	font-weight: bolder;
	font-size: 100px;
	padding: 30px 30px 0 30px;
}
h3 {
	text-align: left;
	font-size: x-large;
	padding: 0 0 0 30px;
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
	color: white;
}
h3 {
	color: white;
}

p {
	color: darkgray;
}
#app {
	font-family: Yu Gothic UI;
	// font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: darkgray;
	overflow: hidden;
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
