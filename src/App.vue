<template>
	<div class="container">
		<div class="search-b">
			<input type="text" id="searchbar" placeholder="Search..." />
		</div>
		<div class="inner-container">
			<h4>Ville</h4>
			<p>Date 14/03/1991</p>
			<div>température</div>
			<p>etat</p>
		</div>
	</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			api_key: "a8f12504ac1bcb5b5bddafaf8e3ddc7c",
		};
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
