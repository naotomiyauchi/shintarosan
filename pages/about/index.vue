<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="about-us-section">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">私たちについて</small>
          <h2>About us</h2>
          <p>Instagramなどの<br class="br-sp">SNSは下記のサイトにまとめてます</p>
        </div>
        <div class="content-column-right">
          <img src="~/assets/images/IMG_3481.jpg" alt="About us" />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: '私たちについて | BAR BARABARU',
  description: '私たちのSNSを紹介します',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: '私たちについて',
    path: route.path
  }
]
</script>


<style lang="scss" scoped></style>