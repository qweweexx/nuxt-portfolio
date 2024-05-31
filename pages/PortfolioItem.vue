<template>
  <div class="portfolio-info">
    <!-- <router-link :to="`/portfolio/${project.id}`">
      <h2 class="portfolio-title">{{ project.name }}</h2>
    </router-link> -->
    <h2 class="portfolio-title">{{ project.name }}</h2>
    <p>프로젝트 유형: {{ project.projectType }}</p>
    <p v-if="project.type">구축 유형: {{ project.type }}</p>
    <p v-if="project.accessibilityMark" class="certification-mark">
      접근성 인증마크: 획득
    </p>
    <div class="period">
      <p class="project-period" v-if="project.duration">
        프로젝트 기간: {{ project.duration }}<br />
        ( {{ project.months }}개월, 총 {{ project.days }}일 )
      </p>
      <p
        class="operation-period"
        v-if="
          project.operation &&
          (project.operation.months || project.operation.days)
        "
      >
        운영 기간: {{ project.operationDuration }}
        <br />
        <span v-if="project.operation.months">
          ( {{ project.operation.months }} 개월,
        </span>
        <span v-if="project.operation.days">
          총 {{ project.operation.days }} 일 )
        </span>
      </p>
    </div>
    <a v-if="project.site" :href="project.site" target="_blank">바로가기</a>
  </div>
</template>

<script>
export default {
  name: "PortfolioItem",
  props: {
    project: Object,
  },
};
</script>

<style lang="scss" scoped>
.portfolio-info {
  line-height: 1.6;

  .portfolio-title {
    margin-bottom: 10px;
    font-size: 1.4rem;
    color: #333;
    font-weight: 600;
  }

  .certification-mark {
    color: crimson;
  }

  .period {
    margin: 10px 0;
  }
}
</style>
