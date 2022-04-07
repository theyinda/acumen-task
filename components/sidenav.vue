<template>
  <nav class="sidebar">
    <div class="logo">
      <img src="../assets/images/logo.png" />
    </div>
    <ul class="side-nav">
      <nuxt-link to="/" class="side-nav_item">
        <p class="side-nav_link">Home</p>
      </nuxt-link>

      <nuxt-link
        to="/allElephants/"
        :class="[
          'side-nav_item elephant',
          $route.name.includes('allElephants-elephant')
            ? 'nuxt-link-exact-active'
            : '',
        ]"
      >
        <p class="side-nav_link">Elephant</p>
      </nuxt-link>
    </ul>
  </nav>
</template>

<script></script>

<style scoped>
.logo{
width: 100%;
margin: 60px auto;
}
.logo img {
  /* width: 50%; */
  display: block;
  margin-left: auto;
  margin-right: auto;
  
}
.sidebar {
  margin: 0;
  padding: 0;
  width: 361px;
  background-color: #ddddff;
  position: fixed;
  height: 100%;
  overflow: auto;
}

.side-nav {
  padding: 0;
}
.side-nav_item {
  width: 100%;
}
.side-nav_link {
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;
  padding: 17px 0px 17px 66px;
  cursor: pointer;
}
a.nuxt-link-exact-active {
  background: #b9b9ff;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;
  color: #fff !important;
}
.sidebar a {
  display: block;
  text-decoration: none;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;
  color: #30425a;
}
@media screen and (max-width: 700px) {
  .sidebar {
    width: 100%;
    height: auto;
    margin: 0 auto;
    position: relative;
    float: center;
  }
  .side-nav_item {
    width: 100%;
  }
}

@media screen and (max-width: 400px) {
  .side-nav_item {
    text-align: center;
    float: none;
  }
  .logo {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 20px 0;
  }
}
</style>
