<template>
  <div id="app">
    <header>
      <div id="burger">
        <router-link to="/" active-class="active">Weatherpls</router-link>
      </div>
      <div id="search">
        <input
          type="text"
          placeholder="Search..."
          id="research"
          v-model="query"
          @keyup.enter="search"
        />
      </div>
      <div id="title">
        <router-link to="/graphic"
          ><img src="../src/assets/bar-chart.png" alt="graphic-logo"
        /></router-link>
      </div>
    </header>
    <router-view />
  </div>
</template>
<script>
export default {
  data: () => ({
    query: ""
  }),
  methods: {
    search() {
      this.$router.push({ path: "/search", query: { city: `${this.query}` } });
    }
  }
};
</script>
<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

body {
  margin: 0;
}
#app {
  font-family: Roboto;
  color: white;
  background: rgb(2, 0, 36);
  background: linear-gradient(
    180deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(64, 64, 179, 1) 0%,
    rgba(100, 174, 241, 1) 100%
  );
}
header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  height: 10vh;
  margin: 0 1.5em;
  .active {
    color: white;
    text-decoration: none;
  }
  #burger {
    display: flex;
    align-items: center;
    font-size: x-large;
  }
  #search {
    display: flex;
    align-items: center;
    justify-content: center;
    #research {
      background: transparent;
      border: 1px solid white;
      border-radius: 4px;
      color: white;
      width: 60%;
      height: 30%;
    }
    .blabla {
      color: white;
      text-decoration: none;
    }
  }
  #title {
    font-weight: bold;
    display: flex;
    align-items: center;
  }
}
</style>
