<template>
  <div :class="['task', { complete: task.done }]">
    <div class="actions">
      <h2 @click="toggleDetail()">{{ task.title }}</h2>
      <div>
        <span @click="deleteTask()" class="material-symbols-outlined">
          delete
        </span>
        <router-link :to="{ name: 'editTask', params: { id: this.task.id } }">
          <span class="material-symbols-outlined"> edit </span>
        </router-link>
        <span @click="toggleDone()" class="material-symbols-outlined done">
          done
        </span>
      </div>
    </div>
    <div v-if="showDetail" class="details">
      <p>{{ task.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task"],
  name: "TasksList",
  data() {
    return {
      showDetail: false,
      url: "http://localhost:3000/tasks/" + this.task.id,
    };
  },
  methods: {
    toggleDetail() {
      this.showDetail = !this.showDetail;
    },
    deleteTask() {
      fetch(this.url, {
        method: "DELETE",
      })
        .then(() => {
          this.$emit("deleteTask", this.task.id);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    toggleDone() {
      fetch(this.url, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          done: !this.task.done,
          title: this.task.title,
          details: this.task.details,
        }),
      })
        .then(() => {
          this.$emit("toggleDone", this.task.id);
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
  emits: ["deleteTask", "toggleDone"],
};
</script>

<style>
.task {
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  background-color: white;
  padding: 15px 20px;
  border-radius: 20px;
  margin: 20px 0px;
  border-left: 8px solid palevioletred;
}
.task.complete {
  border-left: 8px solid green;
}
.task.complete .done {
  color: green;
}
.actions {
  padding: 15px 0px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-symbols-outlined {
  font-size: 25px;
  color: gray;
  margin: 0px 10px;
  cursor: pointer;
}
.material-symbols-outlined:hover {
  color: black;
}
h2 {
  cursor: pointer;
}
.details {
  padding: 15px 0px;
}
</style>
