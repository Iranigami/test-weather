<template>
      <div class="flex w-full justify-between px-[34px] mt-[24px]">
        <a href="/" class="flex gap-[12px] justify-between items-center">
          <img src="../assets/icons/coolicon.svg" class="w-[24px] h-[24px]"/>
          <span class="font-sfregular text-[#8A91AB] text-[16px] leading-[17.71px]">Назад</span>
        </a>
        <button @click="addToFavorites">
          <img src="../assets/icons/Bookmark.svg" class="w-6 h-6"/>

        </button>
      </div>
      <div class="font-sfmedium text-[56px] text-very-white mx-auto w-full text-center mt-[28px]">
        {{ id }}
      </div>
      <div class="font-sflight text-[16px] text-very-white mx-auto w-full text-center mt-4">
        {{ "Облачно" }}
      </div>
      <div class="flex justify-center items-center">
        <span class="from-[rgba(255,255,255,100)] to-[rgba(255,255,255,0)] bg-gradient-to-b bg-clip-text text-[rgba(0,0,0,0)] text-[129.75px] font-sfsemibold"> {{ "+13" }}°</span>
        <img src="../assets/icons/Drizzle.svg" class="w-[191px] h-[191px]"/>
      </div>
      <div class="flex mt-[40px] justify-center items-center gap-2">
        <img src="../assets/icons/barometer.svg" class="w-6 h-6"/>
        <span class="text-very-white text-[16px] font-sflight text-center">
          {{ 765 }} мм рт. ст.
        </span>
      </div>
      <div class="mt-8 text-[#8A91AB] font-sflight text-[16px] leading-[17.71px] text-center">
        Закат в {{ "18:00" }}
      </div>
      <div>
        Что-то пошло не так... Попробуйте обновить страницу
      </div>
    </template>
  

<script setup>

import axios from 'axios';
const route = useRoute()
const id = route.params.name

const dataError = ref(false);

const getWeather = async () => {
    try {
        const weatherData = await axios.get(`https://api.openweathermap.org/data/3.0/onecall?lat=${route.query.lat}&lon=${route.query.lon}&units=metric&appid=3d495272e3d30889ec67b97277bbe87b`)
    } catch {
      dataError.value = true;
    }
};

const weatherData = await getWeather();

</script>