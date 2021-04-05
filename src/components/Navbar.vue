<template>
  <div id="nav">
    <div class="navbar">
      <router-link to="/">Ma météo</router-link>
      <router-link to="/about">About</router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style scoped>
#nav {
  background-color: #242424;
  height: 70px;
}

.navbar {
  width: 85%;
  height: 100%;
  margin: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#nav a {
  font-weight: bold;
  color: #f2f2f2;
  text-decoration: none;
  text-transform: uppercase;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
