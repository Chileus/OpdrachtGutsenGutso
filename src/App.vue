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
}
.content{
  width: 500px;
  margin: 0 auto;
  padding: 48px 16px;
}
input{
  padding: 14px 0px;
  padding-left: 16px;
  border: 1px solid #ddd;
  color: #111;
  font-size: 16px;
  width: 100%;
  box-sizing: border-box;
  outline: none;
}
h2{
  font-family: 'Oswald', sans-serif;
  font-size: 3.5rem;
  text-align: left;
  text-transform: uppercase;
  color: black;
  line-height: 60px;
  margin: 0;
}
button{
  font-size: 16px;
  padding: 16px 24px;
  border: 0px;
  border-radius: 30px;
  width: 100%;
  background-color: black;
  color: white;
  transition: 0.2s;
}
button:hover{
  background-color: grey;
}

input:hover, input:focus, input:target{
  border: 1px solid #000;
}

img{
  bottom: 15px;
  right:20px;
  width:20px;
  position: absolute;
  filter: opacity(50%);
}


</style>
