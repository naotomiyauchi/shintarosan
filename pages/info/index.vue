<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="company-info-section">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">会社情報</small>
          <h2>COMPANY</h2>
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
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: '会社概要 | Jamstack構成のWebサイト制作',
  description: '当社の企業情報や理念をご紹介します。Jamstack技術を駆使した高性能なWebサイト制作でビジネスの成功を支援します。',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: '会社情報',
    path: route.path
  }
]
</script>


<style lang="scss" scoped></style>