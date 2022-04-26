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
      <button>Add Project ➕</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      newProject: { title: "", detail: "", complete: false },
    };
  },
  methods: {
    submit() {
      if (this.newProject.title && this.newProject.detail) {
        fetch("http://localhost:3000/projects", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(this.newProject),
        })
          .then(() => {
            this.newProject.title = this.newProject.detail = "";
            this.$router.push({ name: "home" });
          })
          .catch((error) => console.log(error));
      }
    },
  },
};
</script>

<style>
form {
  max-width: 600px;
  margin: 60px auto 0;
  padding: 30px;
  border-radius: 9px;
  background-color: rgba(198, 223, 245, 0.342);
}
form div {
  margin: 20px 0;
}
form label {
  font-size: 2rem;
  font-weight: bold;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  color: rgb(6, 56, 100);
}
form input,
textarea {
  width: 100%;
  border: 0;
  outline: none;
  padding: 10px;
  border-radius: 9px;
  background-color: rgb(120, 172, 218);
  color: white;
  font-family: "Times New Roman", Times, serif;
  font-size: 2rem;
}
form div.title * {
  display: block;
}
form div.title {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
form div.title label {
  margin-right: 20px;
}
form div.title input {
  font-style: italic;
}
form div.detail label {
  display: block;
  margin-bottom: 20px;
}
form div.detail textarea {
  width: 100%;
  text-indent: 60px;
}
form .submit {
  text-align: center;
  margin: 20px 0 0;
}
form .submit button {
  padding: 10px 20px;
  border-radius: 10px;
  border: 1px solid rgb(31, 86, 134);
  background-color: rgb(6, 56, 100);
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}
form .submit button:active {
  background-color: white;
  color: rgb(6, 56, 100);
}
</style>
