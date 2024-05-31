<template>
  <main>
    <section
      v-for="(skills, index) in skillsData"
      :key="index"
      class="skills"
      :class="`${skills.type}-skills`"
    >
      <h1>{{ skills.title }}</h1>
      <ul>
        <li v-for="(skill, idx) in skills.list" :key="idx">
          <span v-if="skill === 'Voice Modulation'">
            <a
              href="https://www.youtube.com/channel/UC-jOvtcZBLWWJFVLA6WRhGw"
              target="_blank"
            >
              {{ skill }}</a
            >
          </span>
          <span v-else-if="skill === 'Image Generation with Generative AI'">
            <a
              href="https://www.youtube.com/channel/UCyRrpd5Hvu8hDN6EyDWuNUw"
              target="_blank"
            >
              {{ skill }}</a
            >
          </span>
          <span v-else>
            {{ skill }}
          </span>
        </li>
      </ul>
    </section>
  </main>
</template>

<script>
export default {
  name: "MainPage",
  data() {
    return {
      skillsData: [
        {
          type: "web",
          title: "Web Development Skills",
          list: [
            "HTML",
            "CSS",
            "SCSS",
            "JavaScript",
            "Vue",
            "Web Accessibility",
            "Responsive Design",
          ],
        },
        {
          type: "design",
          title: "Design Skills",
          list: ["Photoshop"],
        },
        {
          type: "video-editing",
          title: "Video Editing Skills",
          list: ["Premiere Pro", "After Effects"],
        },
        {
          type: "ai",
          title: "Artificial Intelligence Skills",
          list: [
            "Python",
            "Data Analysis",
            "Data Preprocessing",
            "Machine Learning",
            "Deep Learning",
            "Web Scraping",
            "Voice Modulation",
          ],
        },
      ],
    };
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
@import "@/styles/common.scss";

main {
  @include flex-center;
  text-align: center;
  flex-direction: column;
  padding-top: 1em;
}

.skills {
  margin-bottom: 2rem;

  h1 {
    font-size: 2rem;
    margin: 1rem;
  }

  ul {
    list-style: none;
    padding: 0;

    li {
      margin-bottom: 0.5rem;
      padding: 0.5rem;
      border-radius: 0.5rem;
      background-color: #f2f2f2;
    }
  }
}
</style>
