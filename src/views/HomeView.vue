<template>
  <div class="home">
    <h1>home</h1>
    <div v-for="project in projects" :key="project.id">
      <Project :project="project" @removeProject="removeProject(project.id)" />
    </div>
  </div>
</template>

<script>
import Project from "../components/Project";
export default {
  components: { Project },
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
  },
};
</script>
