<template>
  <div class="w-[270px] h-[190px] rounded-[6px] bg-[#292E44]">
    <span class="text-very-white text-[16px]"> {{ test }}</span>
    <div class="text-very-white text-[16px]"> {{ heat }}</div>
    <img src="{{ icon }}" class="w-[78px] h-[78px]"/>
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
      heat: "+13",
      icon: Clear
    }; 
  }
};

</script>