<template>
  <div class="home">
    <FilterNavigation />
    <div v-for="project in projects" :key="project.id">
      <Project
        :project="project"
        @removeProject="removeProject(project.id)"
        @completeProject="completeProject"
      />
    </div>
  </div>
</template>

<script>
import FilterNavigation from "../components/FilterNavigation";
import Project from "../components/Project";
export default {
  components: {
    FilterNavigation,
    Project,
  },
  name: "HomeView",
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    const fetchProject = async () => {
      const response = await fetch("http://localhost:3000/projects");
      if (response.status !== 200) {
        throw response;
      }
      const projectsArr = await response.json();
      return projectsArr;
    };
    fetchProject()
      .then((responseProjects) => (this.projects = responseProjects))
      .catch((response) => console.log(response.statusText));
  },
  methods: {
    removeProject(removeId) {
      this.projects = this.projects.filter((single) => single.id !== removeId);
    },
    completeProject(completId) {
      const matchProject = this.projects.find(
        (singleProject) => singleProject.id === completId
      );
      matchProject.complete = !matchProject.complete;
    },
  },
};
</script>
<style scoped></style>
