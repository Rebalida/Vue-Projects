<template>
    <main>
        <h1>Weather Report</h1>
        <div class="input-wrap">
            <input v-model="city" 
               @keyup.enter="fetchWeather"
               type="text" 
               placeholder="Enter city name">
            <button @click="fetchWeather" class="btn"><i class="icon ion-android-arrow-forward"></i></button>
        </div>

        <WeatherCard v-if="weather" :weather="weather" />

        <p v-if="error" class="error">{{ error }}</p>
    </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";
import WeatherCard from "@/components/WeatherApp/WeatherCard.vue";

const city = ref("");
const weather = ref("");
const error = ref(null);

const API_KEY = "bd6d6b0c4dc29715d53dac0773a3a482";

async function fetchWeather() {
    error.value = null;
    if(!city.value.trim()){
        error.value = "Please enter a city name";
        return;
    }

    try{
        const response = await axios.get(
            `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=${API_KEY}&units=metric`
        );
        weather.value = response.data;
    } catch (err) {
        error.value = "City not found or API error"
    }
}


</script>

<style lang="scss" scoped>

main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 40px 15px;
    font-size: 18px;
}

h1 {
    letter-spacing: 1px;
    margin-bottom: 16px;
    color: #f0f0f0;
}

.input-wrap {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
  border-radius: 2px;
  padding: 10px 20px;
  background:  rgba(57, 63, 84, 0.8);;
  &:after {
    content: "";
    position: absolute;
    left: 0px;
    right: 0px;
    bottom: 0px;
    z-index: 999;
    height: 2px;
    border-bottom-left-radius: 2px;
    border-bottom-right-radius: 2px;
    background-position: 0% 0%;
    background: linear-gradient(to right, #B294FF, #57E6E6, #FEFFB8, #57E6E6, #B294FF, #57E6E6);
    background-size: 500% auto;
    animation: gradient 3s linear infinite;
  }
}

.input-wrap input {
  flex-grow: 1;
  color: #BFD2FF;
  font-size: 20px;
  line-height: 2.4rem;
  vertical-align: middle;
  background: transparent;
  border: none;
  outline: none; 
  &::-webkit-input-placeholder {
    color: #7881A1;
  }
}

.input-wrap button {
  color:  #7881A1;
  font-size: 20px;
  line-height: 2.4rem;
  vertical-align: middle;
  transition: color .25s;
  &:hover {
    color: #BFD2FF;
  }
}

.error {
  color: red;
  margin-top: 10px;
}

</style>