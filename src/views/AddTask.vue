<template>
  <form @submit.prevent="handleSubmit()">
    <label>Başlık:</label>
    <input type="text" v-model="title" required />
    <label>Detaylar:</label>
    <textarea v-model="detail" required></textarea>
    <button type="submit">Ekle</button>
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      title: "",
      detail: "",
      url: "http://localhost:3000/tasks",
    };
  },
  methods: {
    handleSubmit() {
      let task = {
        id: Math.floor(Math.random() * 1000).toString(),
        title: this.title,
        details: this.detail,
        done: false,
      };
      fetch(this.url, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(task),
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

<style>
form {
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  background-color: white;
  padding: 20px;
  margin: 20px 0px;
  border-radius: 10px;
}
input {
  width: 100%;
  border: none;
  border-bottom: 1px solid gray;
  padding: 10px;
  outline: none;
}
textarea {
  width: 100%;
  height: 120px;
  border: 1px solid grey;
  border-radius: 10px;
  padding: 10px;
  outline: none;
}
label {
  display: block;
  margin: 20px 0px 10px 0px;
  letter-spacing: 1px;
  font-size: 15px;
  font-weight: 500;
  text-transform: uppercase;
}
button {
  display: block;
  margin: 10px auto;
  background-color: burlywood;
  padding: 12px 20px;
  border: none;
  border-radius: 10px;
  font-size: 18px;
  cursor: pointer;
}
button:hover {
  background-color: chocolate;
}
</style>
