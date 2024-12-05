<template>
  <div class="w-[270px] h-[190px] rounded-[6px] bg-[#292E44] justify-center items-center pt-[23px]">
    <div class="text-very-white text-[14px] font-sfregular text-center leading-[15.5px]"> {{ test }}</div>
    <div class="text-very-white text-[40px] font-sfmedium text-center mt-[4px]"> {{ heat }}</div>
    <img src='../assets/icons/Clear.svg' class="w-[100px] h-[100px] mx-auto -mt-[18px]"/>
  </div>
</template>

<script>
import Clear from '../assets/icons/Clear.svg'
import Clouds from '../assets/icons/Clouds.svg'
import Drizzle from '../assets/icons/Drizzle.svg'
import Dust from '../assets/icons/Dust.svg'
import Mist from '../assets/icons/Mist.svg'
import Rain from '../assets/icons/Rain.svg'
import Snow from '../assets/icons/Snow.svg'
import Squall from '../assets/icons/Squall.svg'
import Thunderstorm from '../assets/icons/Thunderstorm.svg'
import Tornado from '../assets/icons/Tornado.svg'

export default { 
  data() { 
    return { 
      test: 'Москва',
      heat: "+13°",
      icon: Clear
    }; 
  }
};

</script>