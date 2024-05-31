<template>
  <main v-if="project">
    <h1>{{ project.name }}</h1>
    <p>{{ project.projectType }}</p>
    <p>{{ project.type }}</p>
    <p v-if="project.accessibilityMark">접근성 마크 획득</p>
    <p>{{ project.duration }}</p>
    <a :href="project.site" target="_blank" v-if="project.site">
      사이트 바로가기
    </a>
  </main>
  <div v-else>프로젝트 정보를 불러오는 중입니다...</div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "PortfolioDetail",
  computed: {
    ...mapGetters(["projects"]),
    project() {
      const id = Number(this.$route.params.id);
      return this.projects.find((project) => project.id === id);
    },
  },
  watch: {
    project(newValue) {
      if (newValue === undefined) {
        this.$router.push({ name: "NotFound" });
      }
    },
  },
};
</script>

<style lang="scss"></style>
