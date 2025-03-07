<template>
  <header :class="headerClass" class="header" :style="headerStyle">
    <div class="container">
      <component :is="isHomePage ? 'h1' : 'div'" class="logo">
        <nuxt-link to="/">
          <img src="~/assets/images/IMG_3475.png" alt="Japalve" class="h-12 w-auto relative top-1 ml-0">
        </nuxt-link>
      </component>
      <nav class="pc-menu">
        <ul>
          <li><nuxt-link to="/">Top</nuxt-link></li>
          <li><nuxt-link to="/about">About</nuxt-link></li>
          <li><nuxt-link to="/service">Menu</nuxt-link></li>
          <li><nuxt-link to="/news">News</nuxt-link></li>
          <li><PrimaryButton to="/contact" label="Contact" :showIcon="false" /></li>
        </ul>
      </nav>
      <div class="hamburger" @click="toggleMenu">
        <span :class="{ open: isMenuOpen }"></span>
        <span :class="{ open: isMenuOpen }"></span>
        <span :class="{ open: isMenuOpen }"></span>
      </div>
    </div>
    <NavigationDrawer :isOpen="isMenuOpen" @close="toggleMenu" />
  </header>
</template>

<script setup lang="ts">
const isMenuOpen = ref(false);
const route = useRoute();
const isHomePage = computed(() => route.path === '/');

const lastScrollY = ref(0);
const isScrollingDown = ref(false);
const isHeaderHidden = ref(false);
const opacity = ref(1);

const handleScroll = () => {
  const currentScrollY = window.scrollY;
  isScrollingDown.value = currentScrollY > lastScrollY.value;
  
  if (currentScrollY > 100 && isScrollingDown.value) {
    isHeaderHidden.value = true;
    opacity.value = 0;
  } else {
    isHeaderHidden.value = false;
    opacity.value = 1;
  }
  
  lastScrollY.value = currentScrollY;
};

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const headerClass = computed(() => ({
  'header-transparent': isHomePage.value && lastScrollY.value < 900,
}));

const headerStyle = computed(() => ({
  opacity: opacity.value,
  transition: 'opacity 0.5s ease-in-out',
}));

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 15px 0;
  z-index: 1000;
  background-color: #000000;
  transition: transform 0.4s ease-in-out, background-color 0.3s ease;
  box-shadow: 0 2px 4px rgba(255, 255, 255, 0.1);
}

.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 90%;
  margin: 0 auto;
}

.pc-menu {
  margin-left: auto;
}

.pc-menu ul {
  display: flex;
  gap: 2em;
  list-style: none;
  margin: 0;
  padding: 0;
}

.pc-menu ul li {
  display: flex;
  align-items: center;
}

.pc-menu ul li a {
  color: white;
}

.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
}

.hamburger span {
  display: block;
  width: 30px;
  height: 3px;
  background-color: white;
  transition: transform 0.3s ease-in-out;
}

/* 画面幅が768px以下の場合、ナビゲーションを非表示にし、ハンバーガーメニューを表示 */
@media (max-width: 768px) {
  .pc-menu {
    display: none;
  }

  .hamburger {
    display: flex;
  }
}

</style>
