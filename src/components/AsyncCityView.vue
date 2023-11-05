<template>
    <div class="flex flex-col flex-1 items-center">
        <!--Banner-->
       <div
           v-if="route.query.preview"
           class=" text-white p-4 bg-weather-secondary w-full text-center"
       >
        <p>
            You are currently previewing this city, click the "+"
            icon to start tracking this city.
        </p>
       </div>
       <!-- Weather Overview-->
       <div
          class="flex flex-col items-center text-white py-12"
       >
       <h1 class="text-4xl mb-2">{{ route.param.city }}</h1>
       <p class="text-sm mb-12">
        {{
            new Date(weatherData.currentTime).toLocaleDateString(
                "en-us",
                {
                    weekday:"short",
                    day:"2-digit",
                    month:"long",
                }
            )
        }}
        {{ 
                new Date(weatherData.currentTime).toLocaleDateString(
                "en-us",
                {
                    timeStyle:"short",
                }
            )
           
         }}
       </p>
       <p class="text-8xl mb-8">
        {{ Math.round( weatherData.current.temp)}}&deg;
       </p>
       <div class="text-center">
        <p>
            Feels like {{ Math.round(weatherData.current.feels_like)}}
        </p>
        <p class="capitalize">
          {{ weatherData.current.weather[0].description }}
        </p>
        <img 
           class="w-[150px] h-auto"
           :src=" 
           `http://openweathermap.org/img/wn/${weatherData.current.weather[0].icon}@2x.png`

           "
           alt=""
        />
       </div>
    
       </div>
    </div>
</template>

<script setup>
import axios from 'axios';
import {useRoute} from "vue-router"

const route = useRoute();
const api_key=import.meta.env.VITE_APP_OPEN_WEATHER_API_KEY;
const getWeatherData = async () => {
    try{ 
     console.log(route);   
     const weatherData = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${route.query.lat}&lon=${route.query.lng}&exclude={part}&appid=${api_key}&units=imperial`);
     console.log(weatherData);

     // cal current data & time
     const localOffset= new Date().getTimezoneOffset()*60000;
     const utc = weatherData.data.current.dt*1000 + localOffset;
     weatherData.data.currentTime=utc+1000*weatherData.data.timezone_offset;

     //cal hourly weather offset
     weatherData.data.hourly.forEach( (hour) => {
        const utc = hour.dt*1000 + localOffset;
        hour.currentTime = utc + 1000*weatherData.data.timezone_offset;
     });

     return weatherData.data;
    }catch (err){
        console.log(err);
    }
};
const weatherData = await getWeatherData();
console.log(weatherData);
</script>
