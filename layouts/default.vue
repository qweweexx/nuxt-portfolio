<template>
  <div id="app">
    <header>
      <nav>
        <nuxt-link to="/">Home</nuxt-link>
        <nuxt-link to="/PortfolioList">Portfolio</nuxt-link>
      </nav>
    </header>
    <nuxt />
    <footer>
      <p>이름: 권도형</p>
      <p>이메일: rnjsehgud84 @ gmail.com</p>
      <p>카카오톡 아이디: rnjsehgud84</p>
      <p>전화번호: 010 6449 2146</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: "DefaultLayout",
};
</script>

<style lang="scss">
@import "@/styles/common.scss";
</style>
