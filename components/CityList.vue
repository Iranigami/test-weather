<template>
    <div v-for="city in favourites" :key="city.id">
      <FavCard :city="city" :icon="iconName" @click="goToCityView(city)" />
    </div>
  </template>
  
  <script setup>
  import axios from "axios";
  import { ref } from "vue";
  import { useRouter } from "vue-router";
  import FavCard from "./FavCard.vue";
  
  const favourites = ref([]);
  const getCities = async () => {
    if (!import.meta.env.SSR) {
      if (localStorage.getItem("favourites")) {
        favourites.value = JSON.parse(
          localStorage.getItem("favourites")
        );
    
        const requests = [];
        favourites.value.forEach((city) => {
          requests.push(
            axios.get(
              `https://api.openweathermap.org/data/2.5/weather?lat=${city.coords.lat}&lon=${city.coords.lon}&lang=ru&units=metric&appid=0d4d8595ad46c5bbc0304d226f1b37b3`
            )
          );
        });
    
        const weatherData = await Promise.all(requests);
    
        weatherData.forEach((value, index) => {
          favourites.value[index].weather = value.data;
          favourites.value[index].icon = `../_nuxt/assets/icons/${value.data.weather[0].main === "Atmosphere" ? value.data.weather[0].id : value.data.weather[0].main}.svg`;

        });
      }
    }
  };


  await getCities();
  
  const router = useRouter();
  const goToCityView = (city) => {
    router.push(`/cities/${city.name}?lon=${city.coords.lon}&lat=${city.coords.lat}`);
  };
  </script>