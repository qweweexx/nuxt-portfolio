<template>
  <main class="portfolio-list">
    <div v-for="year in orderedYears" :key="year" class="year-group">
      <h2>{{ year }}년</h2>
      <ul>
        <li
          v-for="project in groupedProjects[year]"
          :key="project.id"
          class="portfolio-item"
        >
          <PortfolioItem :project="project" />
        </li>
      </ul>
    </div>
  </main>
</template>

<script>
import PortfolioItem from "./PortfolioItem.vue";
import { mapGetters } from "vuex";

export default {
  name: "PortfolioList",
  components: {
    PortfolioItem,
  },
  computed: {
    ...mapGetters(["projects"]),
    computedProjects() {
      if (!this.projects) return [];
      return this.projects
        .map((project) => {
          let duration = this.calculateDuration(
            project.duration,
            project.operationDuration
          );
          if (duration === null) {
            duration = {
              startYear: new Date().getFullYear(),
              months: 0,
              days: 0,
              operation: {
                startYear: new Date().getFullYear(),
                months: 0,
                days: 0,
              },
            };
          }
          return {
            ...project,
            ...duration,
          };
        })
        .sort((a, b) => {
          const aDate = a.duration
            ? new Date(a.duration.split(" - ")[0])
            : new Date(a.operation.startYear);
          const bDate = b.duration
            ? new Date(b.duration.split(" - ")[0])
            : new Date(b.operation.startYear);
          return bDate - aDate;
        });
    },

    groupedProjects() {
      if (!this.computedProjects) return {};
      return this.computedProjects.reduce((grouped, project) => {
        const startYear = project.startYear;
        if (!grouped[startYear]) grouped[startYear] = [];
        grouped[startYear].push(project);
        return grouped;
      }, {});
    },

    orderedYears() {
      return Object.keys(this.groupedProjects).sort((a, b) => b - a);
    },
  },
  methods: {
    calculatePeriod(period) {
      if (!period) {
        console.error("Period is undefined");
        return {
          startYear: new Date().getFullYear(),
          months: 0,
          days: 0,
        };
      }
      const [start, end] = period
        .split(" - ")
        .map((date) => new Date(date.replace(/\./g, "-")));
      if (
        !start ||
        !end ||
        isNaN(start.getFullYear()) ||
        isNaN(end.getFullYear())
      ) {
        console.error("Start or end date is invalid");
        return {
          startYear: new Date().getFullYear(),
          months: 0,
          days: 0,
        };
      }
      const months =
        (end.getFullYear() - start.getFullYear()) * 12 +
        (end.getMonth() - start.getMonth());
      const days = Math.round((end - start) / (1000 * 60 * 60 * 24));
      return {
        startYear: start.getFullYear(),
        months,
        days,
      };
    },

    calculateDuration(duration, operationDuration) {
      const durationPeriod = this.calculatePeriod(duration);
      const operationPeriod = this.calculatePeriod(operationDuration);

      if (!durationPeriod || !operationPeriod) {
        console.error("Duration or operation period is invalid");
        return null;
      }

      let startYear = operationPeriod.startYear;

      if (duration) {
        startYear = durationPeriod.startYear;
      }

      return {
        ...durationPeriod,
        operation: operationPeriod,
        startYear: startYear,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
.portfolio-list {
  text-align: center;
  padding: 2rem;

  h2 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: #333;
  }

  ul {
    list-style: none;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .portfolio-item {
    min-width: 25%;
    margin: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    overflow: hidden;
    transition: box-shadow 0.3s ease, transform 0.3s ease;
    padding: 10px;

    &:hover {
      transform: translateY(-3px);
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    }
  }

  .year-group {
    text-align: center;
    padding: 2rem;
  }
}
</style>
