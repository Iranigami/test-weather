<template>
  <div class="min-h-screen w-[100vw] justify-center min-w-screen">
    <Header></Header>
    <input 
      type="text" 
      v-model="searchQuery"
      @input="getSearchResults"
      class="w-[510px] min-w-[335px] h-[56px] bg-[#2A2F45] text-very-white px-5 mx-auto flex font-sfregular mt-[80px] rounded-[2px] focus:outline-none" 
      placeholder="Укажите город"/>
      <ul class = "absolute text-very-white top-[66px] bg-[#30354B] w-[510px] min-w-[335px] mx-auto right-0 left-0 mt-[136px] font-sfregular z-10 rounded-b-[8px]">
        <li v-for="searchResult in searchResults"
        :key="searchResult.id"
        class = "py-5 px-5 rounded-b-[8px] cursor-pointer hover:bg-[#303F4B]"
        @click = "previewCity(searchResult)"
        >
          {{ searchResult.name }}, {{ searchResult.country }}
      </li>
      </ul>
    <HomeHint></HomeHint>
  </div>
</template>

<script setup>
import FavCard from '~/components/FavCard.vue';
import Header from '~/components/Header.vue';
import HomeHint from '~/components/HomeHint.vue';
import axios from 'axios';


const APIKey = "0d4d8595ad46c5bbc0304d226f1b37b3";
const searchQuery = ref('');
const queryTimeout = ref(null);
const searchResults = ref(null);
const router = useRouter();

const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value!=="") {
      const result = await axios.get(`http://api.openweathermap.org/geo/1.0/direct?q=${searchQuery.value}&limit=5&appid=0d4d8595ad46c5bbc0304d226f1b37b3`);
      searchResults.value = result.data;
      return;
    }
    searchResults.value = null;
  }, 300);
};

const previewCity = (searchResult) => {
  router.push(`/cities/${searchResult.name}?lon=${searchResult.lon}&lat=${searchResult.lat}`)
};
</script>