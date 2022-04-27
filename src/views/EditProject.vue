<template>
  <form @submit.prevent="submit">
    <div class="title">
      <label>Title</label>
      <input type="text" v-model="newProject.title" />
    </div>
    <div class="detail">
      <label>Project Detail</label>
      <textarea cols="30" rows="10" v-model="newProject.detail"></textarea>
    </div>
    <div class="submit">
      <button>Update Project ➕</button>
    </div>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      newProject: { title: "", detail: "", complete: false },
    };
  },
  mounted() {
    const getData = async () => {
      const response = await fetch("http://localhost:3000/projects/" + this.id);
      const objArray = await response.json();
      return objArray;
    };
    getData()
      .then((objArray) => {
        this.newProject.title = objArray.title;
        this.newProject.detail = objArray.detail;
      })
      .catch((err) => console.log(err));
  },
  methods: {
    submit() {
      fetch("http://localhost:3000/projects/" + this.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          title: this.newProject.title,
          detail: this.newProject.detail,
        }),
      }).then(() => this.$router.push({ name: "home" }));
    },
  },
};
</script>

<style></style>
