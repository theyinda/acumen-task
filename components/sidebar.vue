<template>
  <nav class="sidebar">
    <div class="logo">
      <img src="../assets/images/logo.png" />
    </div>
    <ul class="side-nav">
      <nuxt-link to="/" class="side-nav_item">
        <p class="side-nav_link">Home</p>
      </nuxt-link>

      <nuxt-link to="/allElephants/" class="side-nav_item elephant">
        <p class="side-nav_link">Elephant</p>
      </nuxt-link>
    </ul>
  </nav>
</template>

// //
<script>
// export default {
//   async fetch() {
//     this.posts = await fetch(
//       'https://elephantapimary3.herokuapp.com/elephants'
//     ).then((res) => res.json())
//   },
//   data() {
//     return {
//       posts: [],
//     }
//   },
// }
</script>

<style>
.container {
  /* display: flex;
  max-width: 1448px; */
}
.logo img {
  width: 131px;
  margin: 20px 30px;
}
.sidebar {
  background: #ddddff;
  width: 15%;
}
.side-nav {
  padding: 0;
}
.side-nav_item {
  margin: 20px 0 0 0px;
  width: 100%;
}
.side-nav_link {
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 28px;
  padding: 10px 0px 10px 26px;
  cursor: pointer;
}
a.nuxt-link-exact-active {
  background: #b9b9ff;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;
  color: #ffffff !important;
}

.sidebar {
  margin: 0;
  padding: 0;
  /* width: 200px; */
  position: fixed;
  height: 100%;
  overflow: auto;
}

.sidebar a {
  display: block;
  text-decoration: none;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;
  color: #30425a;
}

.sidebar a:hover:not(.active) {
  background: #5959a7;
  color: #ffffff !important;
}


@media screen and (max-width: 700px) {
  .sidebar {
    width: 100%;
    height: auto;
    position: relative;
  }
  .sidebar a {float: left;}

}

@media screen and (max-width: 400px) {
  .sidebar a {
    text-align: center;
    float: none;
  }
}
</style>
