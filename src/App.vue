<template>
  <nav class="navBar">
    <router-link to="/">Yapılacaklar Listesi</router-link>
    <router-link to="/add-task">Yeni Görev Ekle</router-link>
  </nav>
  <router-view />
</template>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
body {
  background-color: cornsilk;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  max-width: 600px;
  margin: 30px auto;
}
nav {
  display: flex;
  justify-content: space-around;

  padding: 10px 0;
}
nav a {
  text-decoration: none;
  color: black;
  font-size: 20px;
}
nav a:hover {
  color: burlywood;
}
a.router-link-active {
  color: burlywood;
  border-bottom: 4px solid burlywood;
  padding-bottom: 4px;
}
</style>
