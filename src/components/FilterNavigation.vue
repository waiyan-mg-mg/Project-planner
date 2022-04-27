<template>
  <div class="filter-navi">
    <button @click="filter('all')" :class="{ active: current === 'all' }">
      All
    </button>
    <button
      @click="filter('complete')"
      :class="{ active: current === 'complete' }"
    >
      Complete
    </button>
    <button
      @click="filter('progress')"
      :class="{ active: current === 'progress' }"
    >
      In Progress
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "all",
    };
  },
  methods: {
    filter(key) {
      this.current = key;
    },
  },
};
</script>

<style>
.filter-navi {
  margin: 10px 0;
}
.filter-navi button {
  padding: 5px;
  margin-left: 5px;
  border: none;
  font-weight: bold;
  background: white;
  cursor: pointer;
  border: 1px solid white;
  color: gray;
}
.filter-navi button.active {
  /* border-color: rgb(253, 200, 200); */
  border-top: 3px solid green;
  border-bottom: 3px solid green;
  color: black;
}
</style>
