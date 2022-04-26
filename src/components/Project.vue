<template>
  <div
    class="project_container"
    :class="{ doneToggle: project.complete }"
    @click.self="toggleDetail = !toggleDetail"
  >
    <div class="flex_container" @click.self="toggleDetail = !toggleDetail">
      <h4 @click.self="toggleDetail = !toggleDetail">
        {{ project.title }} {{ project.complete }}
      </h4>
      <div class="icon_box">
        <span class="trash" @click="removeProject">🗑</span>
        <span class="edit">🖍</span>
        <span
          class="doneToggle"
          @click="toggleComplete"
          :class="{ doneStatus: project.complete }"
          >✔</span
        >
      </div>
    </div>
    <p v-if="toggleDetail">{{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  name: "Project_Com",
  props: ["project"],
  data() {
    return {
      api: "http://localhost:3000/projects/",
      toggleDetail: false,
      isDone: this.project.complete,
    };
  },
  methods: {
    removeProject() {
      fetch(this.api + this.project.id, {
        method: "DELETE",
      })
        .then(() => {
          this.$emit("removeProject");
        })
        .catch((err) => console.log(err));
    },
    toggleComplete() {
      fetch(this.api + this.project.id, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      })
        .then(() => {
          // this.project.complete = !this.project.complete;{simple and cool method}
          this.$emit("completeProject", this.project.id);
        })
        .catch();
    },
  },
};
</script>

<style scoped>
.project_container {
  padding: 15px 25px;
  margin: 15px 0;
  background: rgb(249, 240, 255);
  border-radius: 10px;
  cursor: pointer;
  border-left: 5px solid red;
}
.project_container.doneToggle {
  border-left-color: rgb(113, 255, 113);
}
.project_container h4 {
  margin: 10px 0;
  color: indigo;
}
.project_container p::selection {
  user-select: none;
  background-color: gray;
  color: whitesmoke;
}
.flex_container {
  user-select: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.icon_box {
  cursor: auto;
}
.icon_box span {
  font-size: 2.5rem;
  font-weight: bold;
  margin-left: 10px;
  color: black;
  cursor: pointer;
  transition: transform 500ms;
}
.icon_box span:hover {
  transition: all 500ms;
  display: inline-block;
  transform: translateY(-5px);
}
.icon_box span:active {
  color: black;
}
.icon_box .trash {
  color: crimson;
}
.icon_box .edit {
  color: orangered;
}
.icon_box .doneToggle {
  color: rgb(71, 247, 71);
}
.doneToggle.doneStatus {
  color: gray;
}
.doneToggle.doneStatus:hover {
  transform: translate(0px);
}
</style>
