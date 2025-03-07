<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="services-section">
      <div class="content">
        <small>メニュー/料金</small>
        <h2>Menu / Price</h2>
        <p>詳しいメニューと料金はもっと見るをご覧ください</p>
        <div class="services-grid">
          <div class="service-card" v-for="(service, index) in services" :key="index">
            <div class="service-text">
              <div class="service-number">{{ index < 10 ? '0' + (index + 1) : index + 1 }}</div>
                  <div class="service-title">{{ service.title }}</div>
                  <p class="service-description">{{ service.description }}</p>
              </div>
            </div>
          </div>
        </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: 'メニュー/料金 | BAR BARABARU',
  description: 'メニュー/料金をご紹介します',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: 'サービス',
    path: route.path
  }
]

type Service = {
  title: string;
  description: string;
};

const services: Service[] = [
  { title: '2時間飲み放題 3000円', description: '' },
  { title: '週間イベント', description: '' },
  { title: '各種ショット', description: '' },
  { title: 'ボトル関連', description: '' },
  { title: '単品ドリンク', description: '' },
  { title: 'チャージ料金等', description: '' }
];
</script>


<style lang="scss" scoped></style>