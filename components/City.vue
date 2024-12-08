<template>
      <div class="font-sfmedium text-[56px] text-very-white mx-auto w-full text-center mt-[28px]">
        {{ id }}
      </div>
      <div class="font-sflight text-[16px] text-very-white mx-auto w-full text-center mt-4 capitalize">
        {{ weatherData.data.weather[0].description }}
      </div>
      <div class="flex justify-center items-center">
        <span class="from-[rgba(255,255,255,100)] to-[rgba(255,255,255,0)] bg-gradient-to-b bg-clip-text text-[rgba(0,0,0,0)] text-[129.75px] font-sfsemibold"> {{ Math.floor(weatherData.data.main.temp)}}°</span>
        <img 
          alt="Weather Icon"  
          :src = "iconName" 
          class="w-[191px] h-[191px]"/>
      </div>
      <div class="flex mt-[40px] justify-center items-center gap-2">
        <img 
          src="../assets/icons/barometer.svg" 
          class="w-6 h-6"/>
        <span class="text-very-white text-[16px] font-sflight text-center">
          {{ weatherData.data.main.pressure }} мм рт. ст.
        </span>
      </div>
      <div class="mt-8 text-[#8A91AB] font-sflight text-[16px] leading-[17.71px] text-center">
        Закат в {{ formatDateFromUnix(weatherData.data.sys.sunset) }}
      </div>
    </template>
  

<script setup>

import axios from 'axios';

const route = useRoute()
const id = route.params.name

const dataError = ref(false);
const farourites = ref([]);

const getWeather = async () => {
    try {
        const weatherData = await axios.get(`https://api.openweathermap.org/data/2.5/weather?lat=${route.query.lat}&lon=${route.query.lon}&lang=ru&units=metric&appid=0d4d8595ad46c5bbc0304d226f1b37b3`)
        return weatherData;
    } catch {
      dataError.value = true;
    }
};

const weatherData = await getWeather();
const iconName = `../_nuxt/assets/icons/${weatherData.data.weather[0].main === "Atmosphere" ? weatherData.data.weather[0].id : weatherData.data.weather[0].main}.svg`;

const formatDateFromUnix = (timestamp) => {
  const date = new Date(timestamp * 1000); // Конвертировать секунды в миллисекунды
  var hours = date.getHours().toString();
  var minutes = date.getMinutes().toString();
  if (minutes.length === 1) {
    minutes = '0' + minutes;
  }
  return (hours + ':' + minutes);
};

const addToFavourites = () => {

};

</script>