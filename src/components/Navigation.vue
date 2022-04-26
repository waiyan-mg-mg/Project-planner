<template>
  <div class="navigator">
    <router-link :to="{ name: 'home' }"> <button>Projects</button></router-link>
    <router-link :to="{ name: 'addProject' }">
      <button>New Project</button></router-link
    >
  </div>
</template>
<script>
export default {
  methods: {},
};
</script>

<style scoped>
.navigator {
  display: flex;
  justify-content: center;
}
.navigator button {
  display: block;
  background: none;
  font-size: 1.5rem;
}
.navigator button {
  border: none;
  outline: none;
  color: rgb(255, 145, 0);
  cursor: pointer;
}

.navigator a {
  margin: 0 10px;
  padding-bottom: 5px;
  border-bottom: 4px solid white;
}
.navigator a.router-link-active {
  border-bottom-color: rgb(49, 199, 49);
}
</style>
