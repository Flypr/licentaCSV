<template>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/register">Register</router-link> |
      <router-link to="/login">Login</router-link>
    </div>
</template>

<script>
export default {
    name: 'Nav'
}
</script>

<style scoped>
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a:hover,
#nav a:active {
  font-weight: bold;
  color: #fff;
}

#nav a.router-link-exact-active {
  color: #fff;
}
</style>