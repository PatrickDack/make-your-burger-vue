<template>
  <nav id="nav">
    <router-link to="/" id="logo-url">
      <img :src="logo_src" :alt="app_name" id="logo" />
    </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/orders">Orders</router-link>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  props: ["logo_src", "app_name"],
};
</script>

<style scoped>
#nav {
  background-color: #222;
  border-bottom: 4px solid #111;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav #logo-url {
  margin: auto;
  margin-left: 0;
}

#logo {
  height: 40px;
}

#nav a {
  color: #fcba03;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
}

#nav a:hover {
  color: #fff;
}
</style>
