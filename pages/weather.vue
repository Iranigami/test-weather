<template>
  <div class="bg-[radial-gradient(100%_200%_at_50%_-110%,#5A607C_50%,#161B30_95%)] min-h-screen justify-center min-w-screen">
    <Header></Header>
    <div class="flex w-full justify-between px-[34px] mt-[24px]">
      <a href="/" class="flex gap-[12px] justify-between items-center">
        <img src="../assets/icons/coolicon.svg" class="w-[24px] h-[24px]"/>
        <span class="font-sfregular text-[#8A91AB] text-[16px] leading-[17.71px]">Назад</span>
      </a>
      <button @click="toggleBookmark">
        <img src="../assets/icons/Bookmark.svg" class="w-6 h-6" :class="{ hidden: isBooked }" />
        <img src="../assets/icons/Bookmark_use.svg" class="w-6 h-6" :class="{ hidden: !isBooked }" />
      </button>
    </div>
    <div class="font-sfmedium text-[56px] text-very-white mx-auto w-full text-center mt-[28px]">
      {{ city }}
    </div>
    <div class="font-sflight text-[16px] text-very-white mx-auto w-full text-center mt-4">
      {{ weather }}
    </div>
    <div class="flex justify-center items-center">
      <span class="from-[rgba(255,255,255,100)] to-[rgba(255,255,255,0)] bg-gradient-to-b bg-clip-text text-[rgba(0,0,0,0)] text-[129.75px] font-sfsemibold"> {{ temperature }}</span>
      <img src="../assets/icons/Drizzle.svg" class="w-[191px] h-[191px]"/>
    </div>
    <div class="flex mt-[40px] justify-center items-center gap-2">
      <img src="../assets/icons/barometer.svg" class="w-6 h-6"/>
      <span class="text-very-white text-[16px] font-sflight text-center">
        {{ pressure }} мм рт. ст.
      </span>
    </div>
    <div class="mt-8 text-[#8A91AB] font-sflight text-[16px] leading-[17.71px] text-center">
      Закат в {{ sunset }}
    </div>
    </div>
  </template>

<script>

export default {

  data() { 
    return { 
      city: 'Москва',
      temperature: "+13°",
      weather: "Облачно с прояснениями",
      icon: "",
      pressure: "756",
      sunset: "18:00",
      isBooked: false
    };
  },
  methods: { 
    toggleBookmark() { 
      this.isBooked = !this.isBooked;
      },
    },
  

}


</script>