<template>
  <form @submit.prevent="handleSubmit()">
    <label>Başlık:</label>
    <input type="text" v-model="title" required />
    <label>Detaylar:</label>
    <textarea v-model="detail" required></textarea>
    <button type="submit">Güncelle</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
      url: "http://localhost:3000/tasks/" + this.id,
      done: false,
    };
  },
  mounted() {
    fetch(this.url)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.detail = data.details;
        this.done = data.done;
      })
      .catch((error) => {
        console.error(error);
      });
  },
  methods: {
    handleSubmit() {
      fetch(this.url, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          done: this.done,
          title: this.title,
          details: this.detail,
        }),
      })
        .then(() => {
          this.$router.push({ path: "/" });
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style></style>
