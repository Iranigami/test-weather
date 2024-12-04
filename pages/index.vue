<template>
  <div class="bg-[#161B30] min-h-screen justify-center min-w-screen">
    <Header></Header>
    <input type="text" v-model="query" input="@onQuaryChange" class="w-[510px] h-[56px] bg-[#2A2F45] text-very-white px-5 mx-auto flex font-sfregular mt-[80px]" placeholder="Укажите город"/>
    <HomeHint></HomeHint>
  </div>
</template>

<script>
import FavCard from '~/components/FavCard.vue';
import Header from '~/components/Header.vue';
import HomeHint from '~/components/HomeHint.vue';
</script>