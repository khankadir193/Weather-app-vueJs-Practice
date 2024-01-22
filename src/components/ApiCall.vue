<template>
    <h1>This is the api call components...</h1>
    <h2>{{ weatherData }}</h2>
</template>


<script>
import axios from 'axios';

export default {
    name: "ApiCall",
    data() {
        return {
            weatherData: []
        }
    },
    mounted() {
        const apiKey = "f2b068dd1e4d035bcd5c74bc40d3685b";
        const apiUrl = "https://api.openweathermap.org/data/2.5/weather";
        const latitude = 44.34;
        const longitude = 10.99;

        axios
            .get(apiUrl, {
                params: {
                    lat: latitude,
                    lon: longitude,
                    appid: apiKey,
                    // Add more parameters as needed
                },
            })
            .then((response) => {
                console.log('respone with weathermap...',response);
                this.weatherData = response.data; // Adjust the data extraction based on the API response structure
            })
            .catch((error) => {
                console.error("Error fetching weather data:", error);
            });
    }
}
</script>

<style scoped>
h1 {
    background-color: blue;
    color: aliceblue;
    font-size: 18px;
    font-style: italic;
    font-weight: bold;
}
</style>