<template>
  <form>
    <h2> Log in </h2>
    <div class="form-group">
      <input @blur="handleEmail" v-model="usernameLogin" type="email" class="form-control" placeholder="Email" required>
      <img v-if="correctEmail" class="eye-icon" :src='checksolid' alt='eye' @click='showPassword'>
      <p class='error' v-if="emptyUsername"> May not be empty </p>
    </div>
    <div class="form-group">
      <input @blur="handlePassword" v-model="passwordLogin" @focus="passwordFocus = true" :type="password" class="form-control" placeholder="Password" required>
      <img class="eye-icon" :src='image' alt='eye' @click='showPassword'>
      <p class='error' v-if="emptyPassword"> May not be empty </p>
    </div>
    <button type="submit" @click="doLogin($event)">Log in</button>
    <p v-if="wrongLogin" class="loginError"> The combination of this e-mail address and password is invalid. </p>
  </form>
  <router-link to="/Register" class="button"><div class="registerButton">Register</div></router-link>
</template>

<script>
import eyesolid from "@/assets/eye-solid.svg";
import eyeslashsolid from "@/assets/eye-slash-solid.svg";
import checksolid from "@/assets/check-solid.svg";

export default {
  name: "Login",
  data () {
    return {
      passwordFocus: false,
      emptyUsername: false,
      emptyPassword: false,
      correctEmail: false,
      wrongLogin: false,
      image: eyesolid,
      password: 'password',
      eyesolid,
      checksolid,
      usernameLogin: '',
      passwordLogin: '',
      articleId: String
    }
  },
  props: {
    msg: String,
  },
  methods: {
    doLogin(event){
      event.preventDefault();
      if(this.usernameLogin && this.passwordLogin){
        const article = { email: "eve.aolt@reqres.in", password: "citysl" };
        this.axios.post("https://reqres.in/api/login", article)
          .then(response => console.log(response.status))
          .catch(this.wrongLogin = true)
      }
      if(!this.usernameLogin){
        this.emptyUsername = true;
      }
      if(!this.passwordLogin){
        this.emptyPassword = true;
      }
    },
    showPassword(){
      if(this.password === 'password'){
        this.password = 'text'
        this.image = eyeslashsolid;
      }else{
        this.password = 'password'
        this.image = eyesolid;
      }

    },
    passwordHandler(){
      console.log('passwordchanged')
    },
    handleEmail(){
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      if(re.test(this.usernameLogin)){
        this.correctEmail = true;
      }else{
        this.correctEmail = false;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Oswald&display=swap');

a{
  text-decoration: none;

  .registerButton{
    margin: 10px;
    text-align: center;
    width: 100%;
    padding: 12px 0px;
    background-color: lightgrey;
    border-radius: 30px;
    color:black;
  }
    .registerButton:hover{
      background-color: grey;
    }

}
a:visited{
  color:black;
}



form{
  width:500px;
  margin: 0 auto;

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
