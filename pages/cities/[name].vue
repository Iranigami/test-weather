<template>
    <div class="bg-[radial-gradient(100%_200%_at_50%_-110%,#5A607C_50%,#161B30_95%)] min-h-screen justify-center min-w-screen">
      <Header></Header>
      <div class="flex w-full justify-between px-[34px] mt-[24px]">
        <button @click="backHandler" class="flex gap-[12px] justify-between items-center">
          <img src="../../assets/icons/coolicon.svg" class="w-[24px] h-[24px]"/>
          <span class="font-sfregular text-[#8A91AB] text-[16px] leading-[17.71px]">Назад</span>
        </button>
        <button @click="addToFavorites">
          <img src="../../assets/icons/Bookmark.svg" class="w-6 h-6"/>

        </button>
      </div>
      <Suspense>
        <City/>
      </Suspense>
      </div>
    </template>
  

<script setup>
  const router = useRouter();

  const backHandler = () => {
    router.back();
  };

</script>