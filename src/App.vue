<template>
	<div class="main">
		<div
			class="container"
			:class="{
				/*warm: isWard */
			}"
			:style="{ backgroundImage: `url(${img})` }"
		>
			<div class="filter">
				<div class="search-b">
					<input
						type="text"
						id="searchbar"
						v-model="location"
						placeholder="Search..."
						@keydown="lookForWeather"
					/>
				</div>
				<div class="inner-container" v-if="typeof weather.name != 'undefined'">
					<div class="location-box">
						<div class="location">
							{{ fullLocation }}
						</div>
						<div class="date">
							<!-- Vendredi 12 Août 2022 -->
							{{ setDate }}
						</div>
					</div>

					<div class="weather-box">
						<div class="temperature">
							{{ Math.round(weather.temperature) }}°c
						</div>
						<div class="weather">{{ weather.description }}</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from "axios";
import imgWarm from "@/assets/warm-bg.jpg";
import imgCold from "@/assets/cold-bg.jpg";
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
		lookForWeather(e) {
			if (e.key == "Enter") {
				/* this.weather = {}; */
				console.log(this.weather.main);
				axios
					.post(
						`https://api.openweathermap.org/data/2.5/weather?q=${this.location}&units=metric&appid=${this.api_key}&lang=fr&`
					)
					.then((r) => {
						console.log(r);

						this.weather.name = r.data.name;
						this.weather.country = r.data.sys.country;
						this.weather.description = r.data.weather[0].description;
						this.weather.temperature = r.data.main.feels_like;
						console.log(this.weather);
					})
					.catch((r) => console.log(r));
			}
		},
	},
	computed: {
		setDate() {
			const date = new Date().toLocaleDateString("fr-fr", {
				weekday: "long",
				year: "numeric",
				month: "short",
				day: "numeric",
			});
			return date.charAt(0).toUpperCase() + date.slice(1);
		},
		fullLocation() {
			if (this.weather.country || this.weather.name) {
				return this.weather.name + ", " + this.weather.country;
			}
			return "";
		},
		isWard() {
			return this.weather.temperature > 20;
		},
		img() {
			if (this.weather.temperature > 18) {
				return imgWarm;
			} else {
				return imgCold;
			}
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
	font-family: "Montserrat", sans-serif, Avenir, Helvetica, Arial;

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
	transition: backgroundImage 0.8s ease-in;
	height: 90vh;
	width: 450px;
	border-radius: 10px;
	/* 	border: black 0.5px solid;
	outline: none; */
	color: white;
}

.warm {
	background-image: url("./assets/warm-bg.jpg");
	transition: backgroundImage 0.8s ease-in;
}
.main {
	display: flex;
	height: 100vh;
	justify-content: center;
	align-items: center;
	background: #0f0f0f; /* linear-gradient(
		to bottom,
		rgba(19, 3, 46, 0.75),
		rgb(17, 9, 66),
		rgba(0, 0, 7, 1)
	); */
	/* 	background: linear-gradient(
		to top,
		rgba(244, 245, 228, 0.75),
		rgb(109, 91, 226),
		rgb(67, 67, 231)
	); */
}
.filter {
	background-image: linear-gradient(
		to bottom,
		rgba(0, 0, 0, 0.25),
		rgba(0, 0, 0, 0.75)
	);
	height: 100%;
	border-radius: 10px;
}

.search-b {
	/* max-width: 350px; */
	/* min-height: 100vh; */
	padding: 25px;

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
/* .weather-box {
	/* 	background: rgba(255, 255, 255, 0.2);
	width: 80px;
	height: 80px;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 38px; 
}
.inner-container {
	/* 	width: 100%;
	display: flex;
	align-content: center;
	justify-items: center !important;
	flex-direction: column;
	text-align: center; 
} */
.location {
	color: #fff;
	font-size: 32px;
	font-weight: 500;
	text-align: center;
	text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.date {
	color: #fff;
	font-size: 20px;
	font-weight: 300;
	text-align: center;
	font-style: italic;
}
.weather-box {
	text-align: center;
}

.temperature {
	display: inline-block;
	padding: 10px 25px;
	color: #fff;
	font-size: 102px;
	font-weight: 900;
	text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
	background-color: rgba(255, 255, 255, 0.25);
	border-radius: 16px;
	margin: 30px 0px;
	box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather {
	color: #fff;
	font-size: 48px;
	font-weight: 700;
	font-style: italic;
	text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
