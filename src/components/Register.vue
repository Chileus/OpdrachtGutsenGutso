<template>
  <form>
    <div class='form-header'>
      <h2>Super cool to have you as a customer!</h2>
      <p> As soon as you've completed your registration you will receive a <br><b> 5 euro </b> shopping voucher!</p>
    </div>
    <div class="input-container">
      <input @blur="handleFullname" v-model="fullnameRegister" type="name" class="form-control" placeholder="Full name" required>
    </div>
    <div class="input-container">
      <input @blur="handleEmail" v-model="username" type="email" class="form-control" placeholder="E-mail adress" required>
      <img v-if="correctEmail" class="eye-icon" :src='checksolid' alt='eye' @click='showPassword'>
      <p class='error' v-if="emptyUsername"> May not be empty </p>
    </div>
    <div class="input-container">
      <div class="form-group">
        <input @blur="handlePassword" v-model="passwordRegister" @focus="passwordFocus = true" :type="password" class="password" placeholder="Password" required>
        <img class="eye-icon" :src='eyePass' alt='eye' @click='showPassword'>
      </div>
      <p class='error' v-if="emptyPassword"> May not be empty </p>
      <p class='error' v-if="invalidPassword">Needs a minumum of 8 characters</p>
    </div>
    <div class="input-container">
      <div class="form-group">
        <input @blur="handlePasswordCom" v-model="passwordRegisterCom" @focus="passwordComFocus = true" :type="passwordCom" class="passwordComfirm" placeholder="Comfirm Password" required>
        <img class="eye-icon" :src='eyePassCom' alt='eye' @click='showPasswordCom'>
      </div>
      <p class='error' v-if="passwordNotIdentical">Passwords are not the same</p>
    </div>
    <button type="submit" class="button" @click="doRegister($event)">Register</button>
    <p v-if="errorMessage" class="loginError"> {{errorMessage}} </p>
  </form>
  <div class="login">
    <router-link class="loginlink" to="/"><div>Already have an account?</div></router-link>
  </div>
</template>

<script>

import eyesolid from "@/assets/eye-solid.svg";
import eyeslashsolid from "@/assets/eye-slash-solid.svg";
import checksolid from "@/assets/check-solid.svg";


export default {
  name: "Register",
  props: {
    msg: String,
  },
  data () {
    return {
      eyePass: eyesolid,
      eyePassCom: eyesolid,
      passwordRegisterCom: '',
      passwordRegister: '',
      username: '',
      emptyUsername: false,
      emptyPassword: false,
      eyesolid,
      eyeslashsolid,
      checksolid,
      passwordNotIdentical: false,
      errorMessage: '',
      password: 'password',
      passwordCom: 'password',
      firstTryPassCom: false,
      firstTryPass: false,
      invalidPassword: false
    }
  },
  methods: {
    doRegister(event){
      event.preventDefault();
      if(this.passwordRegisterCom === this.passwordRegister){
        this.passwordNotIdentical = false;
        if(this.passwordRegisterCom && this.username){
          const article = { email: this.username, password: this.passwordRegister };
          this.axios.post("https://reqres.in/api/register", article)
            .then(response => console.log(response.status))
            .catch(error => {
              this.errorMessage = error.response.data.error;
            })
        }
      }else{
        this.passwordNotIdentical = true;
      }
      if(!this.username){
        this.emptyUsername = true;
      }
      if(!this.passwordRegister){
        this.emptyPassword = true;
      }
    },
    showPassword(){
      if(this.password === 'password'){
        this.password = 'text'
        this.eyePass = eyeslashsolid;
      }else{
        this.password = 'password'
        this.eyePass = eyesolid;
      }
    },
    showPasswordCom(){
      if(this.passwordCom === 'password'){
        this.passwordCom = 'text'
        this.eyePassCom = eyeslashsolid;
      }else{
        this.passwordCom = 'password'
        this.eyePassCom = eyesolid;
      }
    },
    handlePassword(){
      this.firstTryPass = true;
      if(this.passwordRegister.length == 0){
        this.emptyPassword = true;
      } else if(this.passwordRegister.length < 8){
        this.invalidPassword = true;
      }
    },
    handlePasswordCom(){
      this.firstTryPassCom = true;
      if(this.passwordRegister != this.passwordRegisterCom){
        this.passwordNotIdentical = true;
      }
    },
    handleEmail(){
      if(this.username == ''){
        this.emptyUsername = true;
      }
    }
  },
  watch: {
    passwordRegister: function (value) {
      if(this.firstTryPass){
        if(value.length < 8 && value.length != 0){
            this.invalidPassword = true;
        }else{
          this.invalidPassword = false;
        }
        if(value.length == 0){
          this.emptyPassword = true;
        }else{
          this.emptyPassword = false;
        }
      }
      if(this.passwordRegister === this.passwordRegisterCom){
        this.passwordNotIdentical = false;
      }
      if(this.firstTryPassCom){
        if(this.passwordRegister !== this.passwordRegisterCom){
          this.passwordNotIdentical = true;
        }
      }
    },
    passwordRegisterCom: function(){
      if(this.firstTryPassCom){
        if(this.passwordRegister === this.passwordRegisterCom){
          this.passwordNotIdentical = false;
        }
        if(this.passwordRegister !== this.passwordRegisterCom){
          this.passwordNotIdentical = true;
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Oswald&display=swap');

a, a:visited{
  text-decoration: none;
  color:black;

}

a:hover{
  color: grey;
}

.login{
  margin-top: 30px;

  .loginlink{
    text-align: center;
  }
}

.form-header{
  margin-bottom: 40px;

  p{
    color:black;
  }
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
  .input-container{
    margin-bottom: 30px;
  }
  .form-group{
    position: relative;
    width: 100%;
  }
}
</style>
