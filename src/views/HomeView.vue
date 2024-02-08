<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
    <div v-else>
      <p v-if="!error">Loading data...</p>
      <span>{{ error }}</span>
    </div>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav.vue";
import SingleProject from "../components/SingleProject.vue";

export default {
  name: "HomeView",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      error: "",
      current: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => (this.error = err));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    handleComplete(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.complete = !p.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((project) => {
          return project.complete;
        });
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => {
          return !project.complete;
        });
      }
      return this.projects;
    },
  },
};
</script>
