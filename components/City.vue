<template>
        <div class="flex w-full justify-between px-[34px] mt-[24px]">
        <button @click="backHandler" class="flex gap-[12px] justify-between items-center">
          <img src="../assets/icons/coolicon.svg" class="w-[24px] h-[24px]"/>
          <span class="font-sfregular text-[#8A91AB] text-[16px] leading-[17.71px]">Назад</span>
        </button>
        <button v-if="!isFavourite()" @click="addToFavourites">
        <img src="../assets/icons/Bookmark.svg" class="w-6 h-6"/>
      </button>
      <button v-if="isFavourite()" @click="deleteFromFavourites">
        <img src="../assets/icons/Bookmark_use.svg" class="w-6 h-6"/>
      </button>
      </div>  
      <div class="font-sfmedium text-[56px] text-very-white mx-auto w-full text-center mt-[28px]">
        {{ id }}
      </div>
      <div class="font-sflight text-[16px] text-very-white mx-auto w-full text-center mt-4 capitalize">
        {{ weatherData.data.weather[0].description }}
      </div>
      <div class="lg:flex lg:justify-center lg:items-center mx-auto lg:gap-[0px] lg:w-[300px] w-[300px] text-center">
        <div class="from-[rgba(255,255,255,100)] to-[rgba(255,255,255,0)] bg-gradient-to-b bg-clip-text text-[rgba(0,0,0,0)] text-[129.75px] font-sfsemibold text-center w-full mx-auto"> {{ Math.floor(weatherData.data.main.temp)}}°</div>
        <img 
          alt="Weather Icon"  
          :src = "iconName" 
          class="w-[191px] h-[191px] lg:mt-[0] mt-[-50px] mx-auto"/>
      </div>
      <div class="flex mt-[40px] justify-center items-center gap-2">
        <img 
          src="../assets/icons/barometer.svg" 
          class="w-6 h-6"/>
        <span class="text-very-white text-[16px] font-sflight text-center">
          {{ Math.floor(weatherData.data.main.pressure * 0.75)}} мм рт. ст.
        </span>
      </div>
      <div class="mt-8 text-[#8A91AB] font-sflight text-[16px] leading-[17.71px] text-center">
        Закат в {{ formatDateFromUnix(weatherData.data.sys.sunset) }}
      </div>
    </template>
  

<script setup>

import axios from 'axios';
import { v4 as uuid } from 'uuid';
const route = useRoute()
const router = useRouter();
const id = route.params.name

const dataError = ref(false);
const favourites = ref([]);

if (!import.meta.env.SSR) {
  if (localStorage.getItem('favourites')) {
    favourites.value = JSON.parse(localStorage.getItem('favourites'));
  }
}

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

const backHandler = () => {
    router.back();
  };

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
  const cityInfo = {
    id: uuid(),
    name: id,
    coords: {
      lat: route.query.lat,
      lon: route.query.lon
    },
    icon: iconName
  }

  favourites.value.push(cityInfo);
  localStorage.setItem('favourites', JSON.stringify(favourites.value));

};

const deleteFromFavourites = () => {
  const index = favourites.value.findIndex(
    (item) =>
      item.coords.lat === route.query.lat && item.coords.lon === route.query.lon
  );
  if (index !== -1) {
    favourites.value.splice(index, 1);
    localStorage.setItem('favourites', JSON.stringify(favourites.value));
  }
};

const isFavourite = () => {
  return favourites.value.some(
    (item) =>
      item.coords.lat === route.query.lat && item.coords.lon === route.query.lon
  );
};

</script>