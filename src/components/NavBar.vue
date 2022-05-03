<template>
  <nav>
    <router-link to="/">
      <img src="" alt="logo" id="logo" />
    </router-link>
    <router-link to="/">Home</router-link> |
    <router-link to="/orders">Orders</router-link>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
};
</script>
