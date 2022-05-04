<template>
  <div id="main-banner">
    <h1>Make Your Burguer</h1>
  </div>
</template>

<script>
export default {
  name: "BannerApp",
};
</script>

<style scoped>
#main-banner {
  align-items: center;
  background-image: url("../../public/img/burger.jpg");
  background-position: 0 -250px;
  background-size: cover;
  display: flex;
  height: 500px;
  justify-content: flex-start;
}

#main-banner h1 {
  color: #fff;
  text-align: center;
  background-color: #222;
  font-size: 60px;
  padding: 20px 40px;
}
</style>
