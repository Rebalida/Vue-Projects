<template>
    <main>
        <div class="city-wrapper">
            <h2>{{ weather.name }}, {{ weather.sys.country }}</h2>
            <img :src="`https://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`" alt="">
            <p class="temperature">{{ weather.main.temp }}°C</p>
        </div>
       
        <div class="details">
            <div class="details-wrapper">
                <div class="details-item">
                    <h4>Feels Like:</h4>
                    <p>{{ weather.main.feels_like }}°C</p>
                </div>
                <div class="details-item">
                    <h4>Weather:</h4>
                    <p>{{ weather.weather[0].description }}</p>
                </div>
                <div class="details-item">
                    <h4>Humidity:</h4>
                    <p>{{ weather.main.humidity }}%</p>
                </div>
            </div>
        </div>
        
    </main>
</template>

<script setup>
    defineProps({
        weather: Object,
    })
</script>

<style lang="scss" scoped>


.city-wrapper{
    display: flex;
    flex-direction: column;
    color: #f0f0f0;
    justify-content: center;
    align-items: center;
}

.city-wrapper img{
    width: 150px;
}

.city-wrapper .temperature{
    font-size: 32px;
}

.details-wrapper{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    
}

.details .details-wrapper .details-item{
    color: #f0f0f0;
    background: #363B4C;
    padding: 20px 50px;
    border-radius: 2px;
    margin: 5px;
}

p{
    text-transform: capitalize;
}

</style>