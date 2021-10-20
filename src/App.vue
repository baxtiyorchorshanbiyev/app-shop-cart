<template>
  <div id="app">
    <div class="nav-bar">
    <div>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
    </div>
    <div>
      <router-link to="/admin">admin</router-link>
    </div>
    </div>
    
    <router-view />
  </div>
</template>
<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.nav-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
}
.nav-bar {
  padding: 30px;
}

.nav-bar a {
  font-weight: bold;
  color: #42b983;
}

.nav-bar a.router-link-exact-active {
  color:  #212427;
}
</style>
