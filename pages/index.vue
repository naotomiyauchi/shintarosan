<template>
  <div>
    <!-- メインビジュアル -->
    <MainVisual />

    <!-- About us セクション -->
    <section class="services-section px-0 py-16 md:py-32" style="background-color: black; color: white;">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">私たちについて</small>
          <h2>About us</h2>
          <p>Instagramなどの<br class="br-sp">SNSは下記のサイトにまとめてます</p>
          <a href="https://lit.link/shintaro0416" target="_blank" rel="noopener noreferrer" class="button-link-primary justify-start mr-auto text-white bg-blue-600 px-4 py-2 rounded-full font-bold transition-colors duration-300 hover:bg-blue-800 h-12 inline-flex items-center mb-4">
           <span class="btn-text">もっと詳しく</span>
           <svg class="inline-block w-4 h-4 text-white relative bottom-[2px] left-[8px]" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
           </svg>
          </a>
        </div>
        <div class="content-column-right">
          <img src="~/assets/images/IMG_3481.jpg" alt="About us" />
        </div>
      </div>
    </section>

    <!-- 事業内容セクション -->
    <section class="services-section px-0 py-6 md:py-12" style="background-color: black; color: white;">
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
          <SecondaryButton to="/service" label="もっと見る" class="mt-4 justify-end ml-auto text-white" />
        </div>
    </section>

    <!-- お知らせ一覧 -->
    <section class="news-section px-0 py-6 md:py-12" style="background-color: black; color: white;">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">お知らせ</small>
          <h2>News</h2>
        </div>
        <div class="content-column-right">
          <ul v-if="newsList && newsList.length" class="news-list text-white">
            <li v-for="news in limitedNewsList" :key="news.id" class="news-item text-white">
              <NuxtLink :to="`/news/${news.id}`">
                <div class="news-date text-white">{{ formatDate(news.publishedAt) }}</div>
                <div class="news-description text-white">{{ news.title }}</div>
              </NuxtLink>
            </li>
          </ul>
          <SecondaryButton to="/news" label="もっと見る" class="mt-4 justify-end ml-auto text-white" />
        </div>
      </div>
    </section>

    <!-- 会社概要 -->
    <section class="company-info-section py-6 md:py-12" style="background-color: black; color: white;">      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">店舗情報</small>
          <h2>Information</h2>
        </div>
        <div class="content-column-right">
          <table>
            <tbody>
              <tr>
                <th>店舗名</th>
                <td>BAR BARABARU<br> BAR SHU-CLIA</td>
              </tr>
              <tr>
                <th>所在地</th>
                <td>熊本県熊本市中央区下通1丁目6-5 Modenaビル <br>熊本県熊本市中央区下通1丁目8-18 銀座ツインビル</td>
              </tr>
              <tr>
                <th>設立</th>
                <td>2021年1月1日</td>
              </tr>
              <tr>
                <th>代表者名</th>
                <td>重永 信太郎</td>
              </tr>
              <tr>
                <th>資本金</th>
                <td>1,000,000円</td>
              </tr>
            </tbody>
          </table>
          <SecondaryButton to="/info" label="もっと見る" class="mt-4 justify-end ml-auto" />
        </div>
      </div>
    </section>

    <!-- お問い合わせ -->
    <section class="contact-section px-0 py-6 md:py-12 bg-[#3A4354] text-white">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">お問い合わせ</small>
          <h2>Contact</h2>
        </div>
        <div class="content-column-right">
          <p>
            従業員も募集しています。<br class="br-sp">お気軽にご相談ください。
          </p>
          <div>
            <PrimaryButton to="/contact" label="お問い合わせする" />
          </div>
        </div>
      </div>
    </section>

  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'top',
  title: 'BAR BARABARU',
  description: '高速表示とセキュアな環境を実現するJamstack構成のWebサイト制作サービス。SEO対策で集客力アップに貢献します。',
});
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

type News = {
  id: string;
  publishedAt: string;
  title: string;
};

// 日付フォーマット関数を作成
function formatDate(dateString: string): string {
  const date = new Date(dateString);
  return date.toLocaleDateString();
}

const { data: newsList } = await useAsyncData('newsList', async () => {
  const { data } = await useMicroCMSGetList<News>({
    endpoint: 'news',
    queries: { fields: ['id', 'publishedAt', 'title'] },
  });

  return data.value?.contents || [];
});

const limitedNewsList = computed(() => {
  return newsList.value?.slice(0, 3) || [];
});
</script>

<style lang="scss" scoped>

section:nth-of-type(odd) {
  background-color: #f8f8f8;
}

section:nth-of-type(even) {
  background-color: #fff;
}

section:last-of-type {
  background-color: #3A4354;
}

// サービスカードのデザイン調整
.service-card {
  background-color: rgba(255, 255, 255, 0.1); // わずかに透ける黒にする
  color: white;
  padding: 20px;
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.3); // 少し目立たせる
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

// サービスカードのテキストを明るく
.service-text {
  color: white;
}

// 数字の部分を強調
.service-number {
  font-size: 24px;
  font-weight: bold;
  color: #ffcc00; // アクセントカラーにする（好みに応じて変更）
}

// リンクやボタンの色を調整
.dark-section a {
  color: #ffcc00; // 目立つ色にする
  text-decoration: none;
  transition: color 0.3s;
}

.dark-section a:hover {
  color: #ff9900; // ホバー時の色変更
}

</style>