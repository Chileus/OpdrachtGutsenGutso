<template>
  <h2> Register </h2>
  <router-link to="/">Login</router-link> |
</template>

<script>

export default {
  name: "Register",
  props: {
    msg: String,
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Oswald&display=swap');
form{
  width:500px;
  margin: 0 auto;
  padding: 48px 16px;
  .loginError{
    padding: 20px;
    background-color: lightgrey;
    color:black;
    border-radius: 5px;
  }
  .error{
    color: red;
    font-size: 14px;
    margin: 5px;
  }

  h2{
    font-family: 'Oswald', sans-serif;
    font-size: 48px;
    text-align: left;
    text-transform: uppercase;
  }
  input{
    padding: 14px 0px;
    padding-left: 26px;
    border: 1px solid #ddd;
    color: #111;
    font-size: 16px;
    width: 100%
  }
  input:hover, input:focus, input:target{
    border: 1px solid #000;
  }

  button{
    font-size: 16px;
    padding: 12px 24px;
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
  .form-group{
    position: relative;
    width: 100%;
    padding-bottom: 30px;
  }
  img{
    bottom: 45px;
    right:0px;
    width:20px;
    position: absolute;
    filter: opacity(50%);
  }
}
</style>
