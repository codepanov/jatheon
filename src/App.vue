<template>
  <div id="app">
    <div id="nav">
      <img src="@/assets/cloud.svg" alt="Jatheon">
      <div class="settings">
        <img src="@/assets/dashboard.svg" alt="Audit">
        <router-link to="/">Audit</router-link>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&family=Open+Sans&display=swap');

body {
  margin: 0;
  padding: 0;
}
#app {
  display: flex;
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#nav {
  /* width: 250px; */
  padding: 20px;
  background-color: #E1E7E9;
}
#nav a {
  font-weight: bold;
  margin-left: 10px;
  text-decoration: none;
}
#nav a.router-link-exact-active {
  color: #00A88D;
}
.settings {
  color: #00A88D;
  font-size: 14px;
  line-height: 18px;
  width: 180px;
  display: flex;
  align-items: center;
  text-align: left;
  margin-top: 25px;
}
@media screen and (max-width: 1170px) {
  #app {
    display: block;
  }
  #nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .settings {
    margin: 0;
  }
}
@media screen and (max-width: 808px) {
  #app {
    width: max-content;
  }
}
</style>