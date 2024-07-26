<template>
  <div class="filterBtn">
    <button @click="filterTask('all')" :class="{ active: filter === 'all' }">
      HEPSİ
    </button>
    <button
      @click="filterTask('completed')"
      :class="{ active: filter === 'completed' }"
    >
      TAMAMLANDI
    </button>
    <button
      @click="filterTask('continue')"
      :class="{ active: filter === 'continue' }"
    >
      DEVAM EDEN
    </button>
  </div>
</template>

<script>
export default {
  name: "FilterTask",
  emits: ["filterTask"],
  props: ["filter"],
  methods: {
    filterTask(filter) {
      this.$emit("filterTask", filter);
    },
  },
};
</script>

<style>
.filterBtn {
  display: flex;
  justify-content: center;
  margin: 20px 0;
}
.filterBtn button {
  padding: 10px 20px;
  margin: 0 5px;
  border: none;
  background-color: #f1f1f1;
  cursor: pointer;
}
.filterBtn button.active {
  background-color: #4caf50;
  color: white;
}
</style>
