<template>
  <div class="lg:w-[510px] w-[335px] mx-auto mt-[26px]">
    <div>
      <img src="/assets/icons/Arrow.svg" class="w-[38px] h-[32px] ml-[40px] lg:ml-[128px] mb-[-17px]"/>
      <span class="font-sfregular text-[#8A91AB] text-[16px] text-center flex mx-auto w-[170px]">
        Начните вводить город,<br/>например,&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
      </span>
      <button @click="hintHandler" class="font-sfregular text-very-white text-[16px] text-center underline decoration-dashed ml-[179px] lg:ml-[266px] absolute mt-[-24px]">
        Ижевск 
      </button>
    </div>
    <div class="mt-[88px] justify-center">
      <span class="font-sfregular text-[#8A91AB] text-[16px] text-center flex mx-auto w-[250px]">Используйте значок «закладки»,</br> чтобы закрепить город на главной</span>
      <img class="mt-[20px] mx-auto" src="/assets/icons/Bookmark.svg"/>
    </div>
  </div>
</template>

<script setup>
  const router = useRouter();

  const hintHandler = () => {
    router.push("/cities/Izhevsk?lon=53.197730742455306&lat=56.86051745")
  };

</script>