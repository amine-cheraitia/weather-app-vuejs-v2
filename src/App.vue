<template>
	<div class="container">
		<div class="search-b">
			<input
				type="text"
				id="searchbar"
				v-model="location"
				placeholder="Search..."
				@keyup="lookForWeather"
			/>
		</div>
		<div class="inner-container">
			<div class="location-box">
				<div class="location">Ville</div>
			</div>
			<p>Date 14/03/1991</p>
			<div class="weather-box">
				<p>température</p>
			</div>
			<p>etat</p>
		</div>
	</div>
</template>

<script>
import axios from "axios";
export default {
	name: "App",
	data() {
		return {
			api_key: "a8f12504ac1bcb5b5bddafaf8e3ddc7c",
			location: "",
			weather: {},
		};
	},
	methods: {
		lookForWeather() {
			axios
				.post(
					`https://api.openweathermap.org/data/2.5/weather?q=${this.location}&units=metric&appid=${this.api_key}&lang=fr&`
				)
				.then((r) => {
					console.log(r);
					this.weather.country = r.data.sys.country;
					this.weather.description = r.data.weather[0].description;
					this.weather.temperature = r.data.main.feels_like;
					console.log(this.weather);
				})
				.catch((r) => console.log(r));
		},
	},
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
#app {
	font-family: "montserrat", sans-serif, Avenir, Helvetica, Arial;
	/* 	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale; */
	/* 	text-align: center;
	color: #2c3e50; */
	/* 	margin-top: 60px; */
}

.container {
	background-image: url("./assets/cold-bg.jpg");
	background-size: cover;
	background-position: bottom;
	transition: 0.4s;
	/* max-width: 450px; */
}

.search-b {
	/* max-width: 350px; */
	min-height: 100vh;
	padding: 25px;
	background-image: linear-gradient(
		to bottom,
		rgba(0, 0, 0, 0.25),
		rgba(0, 0, 0, 0.75)
	);
	margin-bottom: 30px;
}

.search-b #searchbar {
	display: block;
	width: 100%;
	padding: 15px;
	color: #313131;
	border: none;
	outline: none;
	background: none;
	background-color: rgba(255, 255, 255, 0.5);
	border-radius: 0px 16px 0px 16px;
	box-shadow: 0px 0px 8px;
	transition: 0.4s;
}
.search-b #searchbar:focus {
	box-shadow: 0px 0px 16px;
	background-color: rgba(255, 255, 255, 0.75);
	border-radius: 16px 0px 16px 0px;
}
</style>
