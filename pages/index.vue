<template>
  <div class="bg-[#161B30] min-h-screen justify-center min-w-screen">
    <Header></Header>
    <input 
      type="text" 
      v-model="searchQuery"
      @input="getSearchResults"
      class="w-[510px] min-w-[335px] h-[56px] bg-[#2A2F45] text-very-white px-5 mx-auto flex font-sfregular mt-[80px]" 
      placeholder="Укажите город"/>
      <ul class = "absolute text-very-white top-[66px]">
        <li v-for="searchResult in searchResults"
        :key="searchResult.id"
        class = "py-2 cursor-pointer"
        >
        {{ searchResult.name }}
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

const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value!=="") {
      const result = await axios.get(`http://api.openweathermap.org/geo/1.0/direct?q=${searchQuery.value}&limit=5&appid=0d4d8595ad46c5bbc0304d226f1b37b3`);
      searchResults.value = result.data;
      console.log(searchResults);
      return;
    }
    searchResults.value = null;
  }, 300);
};
</script>