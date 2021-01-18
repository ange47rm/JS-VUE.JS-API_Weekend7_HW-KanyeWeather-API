<template>
  <div id='weatherapp'>
        <h2>Weather App</h2>
        <h3>Enter a City</h3>
        <input type='text' id='city' name='city' v-model='cityInput' value=''>
        <br>
        <button v-on:click='getWeather(cityInput)'>Get Weather Info</button>
        <br>
        <h3 v-if='infoFromAPI'> {{ infoFromAPI.name }} </h3>
        <img v-if='iconURL' v-bind:src='iconURL'>
        <h3 v-if='infoFromAPI'> {{ infoFromAPI.weather[0].description }} </h3>
        <h3 v-if='infoFromAPI'>Current temperature: {{ infoFromAPI.main.temp }}°C</h3>
        <h3 v-if='infoFromAPI'>Max temperature: {{ infoFromAPI.main.temp_max }}°C</h3>
        <h3 v-if='infoFromAPI'>Min temperature: {{ infoFromAPI.main.temp_min }}°C</h3>
        <h3 v-if='infoFromAPI'>Humidity: {{ infoFromAPI.main.humidity }}% </h3>

      
  </div>
</template>


<script>

import { APIkey } from "../assets/WeatherAPI_Key"               // APIkey JS file in assets (ignored in .gitignore)

export default {
    name: 'weather-app',
    data () {
        return {
            cityInput: '',
            infoFromAPI: null,
            weatherIcon: null,
            iconURL: null
        }
    },
    props: ['city'],
    methods: {
        async getWeather(cityInput) {
            await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${cityInput}&appid=${APIkey}&units=metric`)
            .then (response => response.json())
            .then (weatherInfoForCity => this.infoFromAPI = weatherInfoForCity)
            this.weatherIcon = this.infoFromAPI.weather[0].icon;                        // wait for line 46 fetch PROMISE before executing this
            this.iconURL = `http://openweathermap.org/img/w/${this.weatherIcon}.png`;
            },
    }
}


</script>

<style>

#weatherapp {
    border: 5px solid rgb(0, 255, 55);
    padding: 10px;
    text-align: center;
    background-color: white;
    margin: 50px;
    background-image: url('../assets/Sky.jpg');
}

</style>