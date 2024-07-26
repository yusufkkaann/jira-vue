<template>
  <div>
    <FilterTask :filter="filter" @filterTask="filteredTask" />
    <div v-for="task in taskFilter" :key="task.id">
      <TasksList
        @deleteTask="deleteTask"
        @toggleDone="toggleDone"
        :task="task"
      />
    </div>
  </div>
</template>

<script>
import FilterTask from "@/components/FilterTask.vue";
import TasksList from "@/components/TasksList.vue";

export default {
  name: "HomeView",
  components: {
    TasksList,
    FilterTask,
  },
  data() {
    return {
      tasks: [],
      filter: "all",
    };
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await fetch("http://localhost:3000/tasks");
        const data = await response.json();
        this.tasks = data;
      } catch (error) {
        console.error(error);
      }
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    toggleDone(id) {
      let myTask = this.tasks.find((task) => task.id === id);
      myTask.done = !myTask.done;
    },
    filteredTask(filter) {
      this.filter = filter;
    },
  },
  async mounted() {
    await this.fetchTasks();
  },
  computed: {
    taskFilter() {
      if (this.filter === "all") {
        return this.tasks;
      } else if (this.filter === "completed") {
        return this.tasks.filter((task) => task.done);
      } else if (this.filter === "continue") {
        return this.tasks.filter((task) => !task.done);
      }
    },
  },
};
</script>
