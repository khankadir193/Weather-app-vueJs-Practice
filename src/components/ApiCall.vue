<template>
    <div class="card-container">
        <div class="card-bg">
            <div class="input-field">
                <input type="text" ref="searchInput" v-model="cityName"  placeholder="search your city" />
                <button @click="focusSearchInput">
                    <img src="../assets/search.png" alt="search-img" />
                </button>
            </div>
            <div class="img-container">
                <img v-if="isClearWeather" src="../assets/clear.png" alt="clear">
                <img v-else-if="isRainWeather" src="../assets/rain.png" alt="rain">
                <img v-else-if="isCloudWeather" src="../assets/clouds.png" alt="clouds">
                <img v-else-if="isDrizzleWeather" src="../assets/drizzle.png" alt="dizzle">
                <img v-else-if="isMistWeather" src="../assets/mist.png" alt="mist">

                <h1>{{ weatherData?.main?.temp  }}°C</h1>
                <h2>{{ weatherData?.name  }}</h2>
            </div>
            <div class="weather-container">
                <div class="left-container">
                    <img src="../assets/humidity.png" alt="">
                    <div class="left-text">
                        <h2>{{ weatherData?.main?.humidity }}%</h2>
                        <h2>Humidity</h2>
                    </div>
                </div>
                <div class="right-container">
                    <img src="../assets/wind.png" alt="">
                    <div class="right-text">
                        <h2>{{ weatherData?.wind?.speed }} km/hr</h2>
                        <h2>Wind Speed</h2>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <h1>{{ weatherData }}</h1>
</template>


<script>
import axios from 'axios';

export default {
    name: "ApiCall",
    data() {
        return {
            weatherData: [],
            cityName: 'Mumbai',
            apiUrl: 'https://api.openweathermap.org/data/2.5/weather',
            apiKey: 'f2b068dd1e4d035bcd5c74bc40d3685b'
        }
    },
    methods: {
        focusSearchInput() {
            //  this.$refs.searchInput.focus();
            console.log('this.cityName...?',this.cityName);
            axios.get(this.apiUrl, {
                params: {
                    q: this.cityName,
                    appid: this.apiKey,
                    units: "metric", // You can adjust units as needed (metric, imperial, etc.)
                },
            }).then((response) => {
                    console.log('respones...weatheropenApi..', response);
                    this.weatherData = response.data;
                })
                .catch((error) => {
                    console.error("Error fetching weather data:", error);
                });
        }
    },
    computed:{
       isClearWeather(){
            let flag = false;
            if(this.weatherData?.weather?.length>0){
              flag = this.weatherData?.weather[0]?.main === 'Clear' ;
            }
            return flag;
        },
        isRainWeather(){
            let flag = false;
            if(this.weatherData?.weather?.length>0){
              flag = this.weatherData?.weather[0]?.main === 'Rain';
            }
            return flag;
        },
        isCloudWeather(){
            let flag = false;
            if(this.weatherData?.weather?.length>0){
              flag = this.weatherData?.weather[0]?.main === 'Clouds' || this.weatherData?.weather[0]?.main === 'Smoke';
            }
            return flag; 
        },
        isDrizzleWeather(){
            let flag = false;
            if(this.weatherData?.weather?.length>0){
              flag = this.weatherData?.weather[0]?.main === 'Drizzle';
            }
            return flag; 
        },
        isMistWeather(){
            let flag = false;
            if(this.weatherData?.weather?.length>0){
              flag = this.weatherData?.weather[0]?.main === 'Mist' || this.weatherData?.weather[0]?.main === 'Haze';
            }
            return flag; 
        },
    },
    // this approach whenever component load on dom
    mounted() {
        const apiKey = "f2b068dd1e4d035bcd5c74bc40d3685b";
        const apiUrl = "https://api.openweathermap.org/data/2.5/weather";
        const cityName = "mumbai"; // Replace with the desired city name
        // this.cityName = "mumbai"

        axios.get(apiUrl, {
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
body {
    all: unset;
    background-color: #eaeaea;

}
.card-container {
    display: flex;
    justify-content: center;
    align-items: center;
    /* height: 100vh; */
    /* Set the container height to 100% of the viewport height */
    /* Your background color */
}

.card-bg {
    background-color: aquamarine;
    width: 30%;
    height: 70vh;
    border-radius: 3rem;
    border: 2px dotted purple;

}

.input-field {
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

.input-field img {
    width: 100%;
}

.input-field button {
    outline: none;
    background: none;
    border: none;
    width: 10%;
}

.img-container img {
    width: 40%;
}

.img-container h1 {
    font-size: 3vw;
    font-stretch: expanded;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin: 0;
}

.img-container h2 {
    font-size: 1vw;
    font-stretch: expanded;
    font-family: Georgia, 'Times New Roman', Times, serif;
    margin: 1vw;
}

.weather-container {
    display: flex;
    width: 100%;
    justify-content: center;
    align-items: center;
    gap: 3rem;
}

.left-container {
    display: flex;
    gap: 1vw;
}

.left-container img {
    width: 30%;
    height: 7vh;
}

.left-container .left-text {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.left-text h2 {
    margin: 0;
    text-align: center;
    font-size: 14px;
}

.right-container {
    display: flex;
    gap: 1vw;
}

.right-container img {
    width: 30%;
    height: 7vh;
}

.right-container .right-text {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    font-family: Georgia, 'Times New Roman', Times, serif;
}

.right-text h2 {
    margin: 0;
    text-align: center;
    font-size: 14px;
}
</style>

<!-- weather api url -->
<!-- https://www.youtube.com/watch?v=MIYQR-Ybrn4 -->

<!-- extra weather status -->
<!-- Haze,Smoke -->