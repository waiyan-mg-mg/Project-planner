<template>
  <div
    class="project_container"
    :class="{ done: inProgress }"
    @click.self="toggleDetail = !toggleDetail"
  >
    <div class="flex_container" @click.self="toggleDetail = !toggleDetail">
      <h4 @click.self="toggleDetail = !toggleDetail">{{ project.title }}</h4>
      <div class="icon_box">
        <span class="trash" @click="this.$emit('removeProject')">🗑</span>
        <span class="edit">🖍</span>
        <span
          class="done"
          @click="this.inProgress = !this.inProgress"
          :class="{ doneStatus: inProgress }"
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
      toggleDetail: false,
      inProgress: false,
    };
  },
  methods: {},
};
</script>

<style scoped>
.project_container {
  padding: 15px 25px;
  margin: 15px 0;
  background: rgb(230, 230, 230);
  border-radius: 10px;
  cursor: pointer;
  border-left: 3px solid red;
}
.project_container.done {
  border-color: green;
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
.icon_box .done {
  color: green;
}
.done.doneStatus {
  color: gray;
}
.done.doneStatus:hover {
  transform: translate(0px);
}
</style>
