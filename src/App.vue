<template>
  <div class="content">
    <router-view />
  </div>
</template>

<script>


export default {
  name: "App"
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.content{
  width: 500px;
  margin: 0 auto;
  padding: 48px 16px;
}
</style>
