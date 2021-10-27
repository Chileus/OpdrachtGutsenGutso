<template>
  <form>
    <h2>Log in</h2>
    <div class="input-container">
      <div class="form-group">
        <input ref='email' @blur="handleEmail" v-model="usernameLogin" type="email" class="form-control" placeholder="E-mail address" required>
        <img v-if="correctEmail == true" class="eye-icon" :src='checksolid' alt='eye' @click='showPassword'>
      </div>
      <p class='error' v-if="emptyUsername"> May not be empty </p>
      <p class='error' v-if="!correctEmail"> Must be a valid e-mail adress</p>
    </div>
    <div class="input-container">
      <div class="form-group">
        <input @blur="passwordHandler" v-model="passwordLogin" @focus="passwordFocus = true" :type="password" class="form-control" placeholder="Password" required>
        <img class="eye-icon" :src='image' alt='eye' @click='showPassword'>
      </div>
      <p class='error' v-if="emptyPassword"> May not be empty </p>
      <p class='error' v-if="invalidPassword">Needs a minumum of 8 characters</p>
    </div>
    <button type="submit" class="button" @click="doLogin($event)">Log in</button>
    <p v-if="wrongLogin" class="loginError"> The combination of this e-mail address and password is invalid. </p>
    <router-link to="/Register"><div class="button registerButton">Make an account</div></router-link>
  </form>

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
      invalidPassword: false,
      correctEmail: Boolean,
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
        //"eve.holt@reqres.in"
        //"cityslicka"
        const article = { email: this.usernameLogin, password: this.passwordLogin};
        this.axios.post("https://reqres.in/api/login", article)
          .then(() => window.location.href = "https://www.gutsgusto.com/en")
          .catch(() => this.wrongLogin = true)
      }
      if(!this.usernameLogin){
        this.emptyUsername = true;
        this.focusInputEmail();
      }
      else if(!this.passwordLogin){
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
      this.firstTry = true;
      if(this.passwordLogin.length == 0){
        this.emptyPassword = true;
      }else{
        this.emptyPassword = false;
      }
      if(this.passwordLogin.length < 8 && this.passwordLogin.length !=0){
        this.invalidPassword = true;
      }else{
        this.invalidPassword = false;
      }
    },

    handleEmail(){
      if(this.usernameLogin == ''){
        this.emptyUsername = true;
      }else{
        this.emptyUsername = false;
        var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
        if(re.test(this.usernameLogin)){
          this.correctEmail = true;
        }else{
          this.correctEmail = false;
        }
      }
    },
    focusInputEmail() {
      this.$refs.email.focus();
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
    text-align: center;
    width: 100%;
    padding: 12px 0px;
    background-color: #f0f0f0;
    border-radius: 30px;
    color:black;
  }
}

a:visited{
  color:black;
}

.button{
  margin: 10px 0;
}

form{
  max-width:500px;
  margin: 0 auto;
  padding: 48px 16px;
  h2{
    margin-bottom: 10px;
  }
  img{
    bottom: 15px;
  }
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
  .form-group{
    position: relative;
    width: 100%;
  }
  .input-container{
    padding: 10px 0;
  }
}
</style>
