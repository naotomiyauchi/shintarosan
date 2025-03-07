<template>
  <section class="relative w-full h-[85vh] overflow-hidden flex justify-start bg-gray-100 px-0 pb-30">
    <div class="mv-area relative z-10 text-left max-w-1280 w-full mx-auto flex flex-col">
      <div class="max-md:text-3xl text-5xl font-bold mb-4 leading-tight text-white">
        BARABARU
      </div>
      <p class="text-lg mb-8 leading-relaxed text-white">
        熊本下通で<br class="br-sp">圧倒的パフォーマンスを体験
      </p>
    </div>
    <div class="absolute top-0 left-0 w-full h-full">
      <img src="/assets/images/IMG_3473.jpg" alt="Main Visual" class="w-full h-full object-cover md:hidden" />
      <img src="/assets/images/IMG_3473.jpg" alt="Main Visual" class="hidden md:block w-full h-full object-cover" />
    </div>
  </section>
</template>

<style lang="scss" scoped>
.mv-area {
  max-width: 1280px;
  width: 100%;
  margin: auto;
}

@media (max-width: 768px) {
  .mv-area {
    margin: 0 16px;
    align-self: end;
  }
}
</style>
