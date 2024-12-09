<template>
  <div class="w-[270px] h-[190px] rounded-[6px] bg-[#292E44] justify-center items-center pt-[23px]">
    <div class="text-very-white text-[14px] font-sfregular text-center leading-[15.5px]"> {{ city.name }}</div>
    <div class="text-very-white text-[40px] font-sfmedium text-center mt-[4px]"> {{ Math.floor(city.weather.main.temp) }}</div>
    <img :src="city.icon" class="w-[100px] h-[100px] mx-auto -mt-[18px]"/>
  </div>
</template>

<script setup>
defineProps({
  city: {
    type: Object,
    default: () => {},
  },
});
</script>