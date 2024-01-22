<template>
    <div class="card-container">
        <div class="card-bg">
            <div class="input-field">
                <input type="text" placeholder="search your city" />
                <img src="../assets/search.png" alt="search-img" />
            </div>
            <div class="img-container">
                <img src="../assets/clouds.png" alt="clouds">
                <h1>22°C</h1>
                <h2>Mumbai</h2>
            </div>
            <div class="weather-container">
                <div class="left-container">
                    <img src="../assets/humidity.png" alt="">
                    <div class="left-text">
                        <h2>50%</h2>
                        <h2>Humidity</h2>
                    </div>
                </div>
                <div class="right-container">
                    <img src="../assets/wind.png" alt="">
                    <div class="right-text" >
                        <h2>15 km/hr</h2>
                        <h2>Wind Speed</h2>
                    </div>
                </div>
            </div>
        </div>
    </div>
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
        const cityName = "mumbai"; // Replace with the desired city name

        axios
            .get(apiUrl, {
                params: {
                    q: cityName,
                    appid: apiKey,
                    units: "metric", // You can adjust units as needed (metric, imperial, etc.)
                },
            })
            .then((response) => {
                console.log('respones...weatheropenApi..', response);
                this.weatherData = response.data;
            })
            .catch((error) => {
                console.error("Error fetching weather data:", error);
            });
    }
}
</script>

<style scoped>
/* body {
    padding: 0;
    margin: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;

    background-color: #fa0707;
} */
body{
    all: unset;
}




.card-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    /* Set the container height to 100% of the viewport height */
    background-color: #eaeaea;
    /* Your background color */
}

.card-bg {
    background-color: aquamarine;
    width: 30%;
    height: 70vh;
    border-radius: 3rem;
    border: 2px dotted purple;

}

.input-field{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 1vw;
}

.input-field input {
    width: 50%;
    padding: 12px 10px;
    margin: 1rem;
    border-radius: 2vw;
    outline: none;
    border: none;
}

.input-field img{
    width: 7%;
}

.img-container img{
    width: 40%;
}

.img-container h1{
    font-size: 3vw;
    font-stretch: expanded;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin: 0;
}

.img-container h2{
    font-size: 1vw;
    font-stretch: expanded;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin: 1vw;
}

.weather-container{
    display: flex;
    width: 100%;
    justify-content: center;
    align-items: center;
}

.left-container{
    display: flex;
    gap: 1vw;
}

.left-container img{
    width: 30%;
    height: 8vh;
}

.left-container .left-text{
    display: flex;
    flex-direction: column;
    /* justify-content: center; */
    /* align-items: center; */
}

.left-text h2{
    margin: 0;
    text-align: center;
    font-size: 14px;
}

.right-container{
    display: flex;
    gap: 1vw;
}

.right-container img{
    width: 30%;
    height: 8vh;
}

.right-container .right-text{
    display: flex;
    flex-direction: column;
    /* justify-content: center; */
    /* align-items: center; */
}

.right-text h2{
    margin: 0;
    text-align: center;
    font-size: 14px;
}

</style>