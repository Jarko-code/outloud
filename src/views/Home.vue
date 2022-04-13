<template>
 <div class="container">
   <div class="row">
     <div class="col-lg-12">
       <div class="register" v-show="state.form">
        <form  class="register-form">
          <div class="row">
            <h1 class="col-lg-12">Registration Form</h1>
          </div>
          <fieldset>
            <div class="row">
              <div class="col-lg-12">
                <div class="label-animation ">
                  <input class="input" type="email" placeholder=" " v-model="state.email" :class="{ error: v$.email.$errors.length }"> 
                  <label>Email</label>
                  <span class="focus-border"></span>
                </div>
                <span v-if="v$.email.$error" class="error-message">
                  {{ v$.email.$errors[0].$message }}
                </span>
              </div>
            </div>
          </fieldset>
          <fieldset>
            <div class="row">
              <div class="col-lg-6 col-md-12">
                <div class="label-animation margin-bottom">
                  <input class="input" type="text" placeholder=" " v-model="state.firstName" :class="{ error: v$.firstName.$errors.length }">
                  <label>First name</label>
                  <span class="focus-border"></span>
                </div>
                <span v-if="v$.firstName.$error" class="error-message">
                  {{ v$.firstName.$errors[0].$message }}
                </span>
              </div>
              <div class="col-lg-6 col-md-12">
                <div class="label-animation">
                  <input class="input" type="text" placeholder=" " v-model="state.lastName" :class="{ error: v$.lastName.$errors.length }">
                  <label>Second name</label>
                  <span class="focus-border"></span>
                </div>
                <span v-if="v$.lastName.$error" class="error-message">
                  {{ v$.lastName.$errors[0].$message }}
                </span>
              </div>
            </div>
          </fieldset>
          <fieldset class="margin-bottom-0">
            <div class="row">
              <div class="col-lg-6 col-md-12">
                <Popper>
                  <div>
                    <label for="language" class="select margin-bottom" :class="{ error: v$.language.$errors.length }">
                      <div>
                        <div v-if="state.language.length" >
                          <p>
                            {{state.language.join(' ')}}
                          </p>
                          <input type="text" hidden v-model="state.language">
                        </div>
                        <div v-else >
                          Language
                        </div>
                      </div>
                    </label>
                    <span v-if="v$.language.$error" class="error-message">
                      {{ v$.language.$errors[0].$message }}
                    </span>    
                  </div>
                  <template #content>
                    <div class="options">
                      <div @click='getLang' @blur="!state.hideLang" v-for="(lang, index) in state.options" :key="index">
                        <div>
                          <img :src="require(`../assets/${lang.img}`)" alt="">
                          <span>{{lang.name}}</span>
                        </div>
                      </div>
                    </div>
                  </template>
                </Popper>
              </div>
              <div class="col-lg-6 col-md-12">
                <Popper>
                  <div>
                    <label for="language" class="select margin-bottom" :class="{ error: v$.country.$errors.length }">
                      <div>
                        <div v-if="state.country.length" >
                          <p>
                            {{state.country.join(' ')}}
                          </p>
                          <input type="text" hidden v-model="state.country">
                        </div>
                        <div v-else >
                          Country    
                        </div>
                      </div>
                    </label>
                    <span v-if="v$.country.$error" class="error-message">
                      {{ v$.country.$errors[0].$message }}
                    </span>
                  </div>
                  <template #content>
                    <div class="options overflow">
                      <div @click='getCountry' @blur="!state.hideCountry" v-for="(country, index) in countries" :key="index">
                        <div @keyup='nextItem'>
                          <span  :class='{"active-item": state.currentItem === country.name}'>{{country.name}}</span>
                        </div>
                      </div>
                    </div>
                  </template>
                </Popper>
              </div>
            </div>
          </fieldset>
          <fieldset>
            <div class="row">
              <div class="col-lg-6 col-md-12">
                <div class="label-animation">
                  <div class="password-style margin-bottom"> 
                    <input class="input" placeholder=" " :type="state.passwordFieldType" v-model="state.password" :class="{ error: v$.password.$errors.length }">
                    <a @click.prevent="showPassword">
                      <img src="../assets/Path.svg" alt="">
                    </a>
                    <label>Password</label> 
                    <span class="focus-border"></span>
                  </div>
                </div>
                <span v-if="v$.password.$error" class="error-message">
                  {{ v$.password.$errors[0].$message }}
                </span>
              </div>
              <div class="col-lg-6 col-md-12">
                <div class="label-animation">
                  <div class="password-style"> 
                    <input class="input" placeholder=" " :type="state.passwordConfirmedFieldType" v-model="state.confirmPassword" :class="{ error: v$.confirmPassword.$errors.length }">
                    <a @click.prevent="showConfirmedPassword">
                      <img src="../assets/Path.svg" alt="">
                    </a>
                    <label>Confirm Password</label> 
                    <span class="focus-border"></span>
                  </div>
                </div>
                <span v-if="v$.confirmPassword.$error" class="error-message">
                  {{ v$.confirmPassword.$errors[0].$message }}
                </span>
              </div>
            </div>
          </fieldset>
          <div class="row">
            <div>
              <div class="flex-layout-profile">
                <label for="">Private profil</label>
                <div class="private-profile">
                  <input type="checkbox" v-model="state.profile" id="switch" @click="privateProfile" :class="{ error: v$.profile.$errors.length }">
                  <span v-if="v$.profile.$error" class="error-message">
                    {{ v$.profile.$errors[0].$message }}
                  </span>
                  <label for="switch"></label>
                  <p class="yes" v-if="state.checkedProfile">YES</p>
                  <p class="no" v-else>NO</p>
                </div>
              </div>
            </div>
            <div class="flex-layout-register">
              <button class="desktop" type="submit" @click.prevent="register">Sign up</button>
              <div class="agreement">
                <input type="checkbox" v-model="state.agreement">
                <p>Creating an account means you’re okay with our Privacy Policy.</p>
                <span v-if="v$.agreement.$error" class="error-message">
                  {{ v$.agreement.$errors[0].$message }}
                </span>
              </div>
              <button class="mobile" type="submit" @click.prevent="register">Sign up</button>
            </div>
          </div>
        </form>
      </div>
      <transition name="show">
        <div v-show="state.notification" class="container">
          <div class="row">
            <div class="col-lg-12">
              <div  class="notification">
                <div class="notification-content">
                  <div class="img">
                    <img src="../assets/Success.svg" alt="">
                  </div>
                  <h3>Success registration</h3>
                  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris lobortis gravida ex, at maximus lorem condimentum ut. Cras purus mauris, convallis vitae sollicitudin sed, fringilla lobortis lorem. </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition>
     </div>
   </div>
 </div>



  
</template>

<script>
import {reactive, computed, ref, onMounted} from 'vue'
import axios from 'axios'
import useVuelidate  from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'
import Popper from "vue3-popper";
export default {
  name: 'Home',
  components: {
    Popper,
  },
  setup() {
    //reactive state
    const state = reactive({
      email: '',
      firstName: '',
      lastName: '',
      language: [],
      country: [],
      options: [
        {name: 'Slovak', img: 'slovakia.svg'},
        {name: 'English', img: 'english.svg'},
      ],
      hideLang: '',
      hideCountry: '',
      password: '',
      passwordFieldType: 'password',
      passwordConfirmedFieldType: 'password',
      confirmPassword: '',
      profile: '',
      checkedProfile: false,
      agreement: '',
      notification: false,
      form: true,
      currentItem: 1,
    })

    //get countries
    let countries = ref([])
    onMounted(async() => {
      await axios.get('https://restcountries.com/v2/all?fields=name').then(response => {
        countries.value = response.data
      }),

      // keyup event
      document.addEventListener("keyup", nextItem);
    })

    //set Lang and country to popper hide input
    function getLang(event){
      let a = event.target.outerText
      state.language.push(a)
      state.hideLang = true
    }
    function getCountry(event){
      let b = event.target.outerText
      state.country.push(b)
      state.hideCountry = true
    }

    //keyup function
    function nextItem (event) {
    	if (event.keyCode == 38) {
      	this.currentItem--
      } else if (event.keyCode == 40) {
      	this.currentItem++
      }
    }

    //show/hide password
    const showPassword = () => state.passwordFieldType = state.passwordFieldType === "password" ? "text" : "password";
    const showConfirmedPassword = () => state.passwordConfirmedFieldType = state.passwordConfirmedFieldType === "password" ? "text" : "password";
    
    //toggle checkbox
    const privateProfile = () => {
      state.checkedProfile = !state.checkedProfile
    }
    
    //validation rules
    const rules = computed( () => {
      return {
        firstName: { required }, 
        lastName: { required }, 
        email: { required, email },
        country: {required},
        language: {required},
        password: {required},
        confirmPassword: {required},
        profile: {required},
        agreement: {required},
      }
    })

    //v$ definition
    let v$ = useVuelidate (rules, state)

    //register function with validation
    function register(){
      this.v$.$validate()
      if(!this.v$.$error){
        let submitstate = {
          email: state.email,
          firstName: state.firstName,
          lastName: state.firstName,
          language: state.language,
          country: state.country,
          password: state.password,
          confirmPassword: state.confirmPassword,
          profile: state.profile,
          agreement: state.agreement
        }
        console.log('Submited state:', submitstate)
        state.notification = true,  
        state.form = false
        setTimeout( () => {
          state.notification = false
          state.form = true
        }, 3500)
      }
      else{
        console.log('error')
      }

    }
    //return statement
    return {
      state, showPassword, showConfirmedPassword, privateProfile, register, v$, countries, getLang, getCountry, nextItem
    }
  }
  
}
</script>

<style lang="scss">
@import '../assets/mixins.scss';
@import '../assets/variables.scss';

.register{
  position: absolute;
  min-width: 874px;
  max-height: 887px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background: #FFF;
  box-shadow: 0px 40px 60px -33px rgba(0, 0, 0, 0.04);
  border-radius: 25px;
  padding: 94px 106px 140px;
  @media #{$mobile}{
    position: unset;
    max-height: unset;
    min-width: unset;
    transform: unset;
    text-align: left;
    padding: 25px 20px;
  }
  h1{
    font-style: normal;
    font-weight: 500;
    font-size: 60px;
    line-height: 78px;
    letter-spacing: -0.02em;
    color: #333;
    margin-bottom: 58px !important;
    @media #{$very_small}{
      font-size: 30px;
      margin-bottom: 29px !important;
    }
  }
  .register-form{
    fieldset{
      border: none;
      padding: 0;
      margin-bottom: 26px;
      input, select{
        width: 100%;
        padding-left: 18px;
        @include inputs-default;
        @media #{$mobile}{
          padding-left: 20px;
        }
      }
      .inline-block{
        display: block !important;
      }
      .select{
        font-weight: 500;
        padding-left: 18px;
        color: #b1aaaa;
        font-family: 'DM Sans';
        @include inputs-default;
        div{
          position: absolute;
          top: 50%;
          transform: translateY(-50%);
        }
        .no-wrap{
          white-space: nowrap;
        }
      }
      input[type=email]{
        width: 100%;
        display: block;
        padding-left: 18px;
        @include inputs-default;
        @media #{$mobile}{
          padding-left: 20px;
        }
      }
      input:hover, select:hover{
        border: 1px solid #D5DBE2;
      }

      input:focus{
        background: #fff;
        opacity: 0.6;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      }
      .margin-bottom{
        margin-bottom: 26px;
         @media #{$mobile}{
           margin-bottom: 20px;
        }
         @media #{$laptop}{
           margin-bottom: 0px;
        }
      }
    }
    .flex-layout-profile{
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #F1F3F5;
      padding-bottom: 29px;
      @media #{$mobile}{
        padding-left: 21px;
      }
      label{
        color: #1C2D41;
        font-weight: 500;
      }
      .private-profile{
        display: flex;
        align-items: center;
        position: relative;
        input{
          width: 0;
          height: 0;
          visibility: hidden;
        }
        label {
          display: block;
          width: 60px;
          height: 30px;
          background-color: #F2F5F8;
          border-radius: 10px;
          position: relative;
          cursor: pointer;
          transition: 0.5s;
          &::after{
            content: "";
            width: 19px;
            height: 24px;
            background-color: #fff;
            position: absolute;
            border-radius: 7px;
            top: 3px;
            left: 5px;
            transition: 0.5s;
          }
        }
        input:checked + label:after {
          left: calc(100% - 5px);
          transform: translateX(-100%);
        }
        input:checked + label {
          background-color: #004EEF;
        }
        .no{
          position: absolute;
          right: 11px;
          font-weight: 700;
          font-size: 11px;
          transition: 0.4s;
        }
        .yes{
          position: absolute;
          left: 11px;
          font-weight: 700;
          font-size: 11px;
          color: #fff;
          transition: 0.4s;
        }
        p{
          margin: 0;
        }
      }
    }
    .flex-layout-register{
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-top: 29px;
      @media #{$mobile}{
        display: block;
        padding-top: 21px;
        .desktop{
          display: none;
        }
      }
      @media #{$laptop}{
        .mobile{
          display: none !important;
        }
      }
      .mobile{
        display: block;
        width: 100%;
        margin-top: 30px;
      }
      button{
        border: none;
        outline: none;
        width: 268px;
        height: 62px;
        background: linear-gradient(269.72deg, #004EEF 0.1%, #8600EF 96.94%);
        box-shadow: 0px 4px 14px rgba(0, 78, 239, 0.19);
        border-radius: 16px;
        color: #fff;
        cursor: pointer;
        position: relative;
        z-index: 1;
        &::before{
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          content: '';
          background: linear-gradient(269.72deg, #8600EF 0.1%, #004EEF 96.94%);
          z-index: -1;
          transition: opacity 0.5s linear;
          opacity: 0;
          box-shadow: 0px 4px 14px rgba(0, 78, 239, 0.19);
          border-radius: 16px;
        }
        &:hover::before{
          opacity: 1;
        }
      }
      .agreement{
        display: flex;
        align-items: center;
        text-align: left;
        margin-left: 37px;
        @media #{$mobile}{
          margin-left: 0px;
        }
        input[type="checkbox"] {
          -webkit-appearance: none;
          appearance: none;
          background-color: #F2F5F8;
          margin: 0;
          width: 21px;
          height: 22px;
          border-radius: 6px;
          display: grid;
          place-content: center;
        }
        input[type="checkbox"]::before {
          content: "";
          width: 9px;
          height: 7.15px;
          clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
          transform: scale(0);
          transform-origin: bottom left;
          transition: 120ms transform ease-in-out;
          background-color: #fff;
        }
        input[type="checkbox"]:hover {
          border: 1px solid #D5DBE2;
        }
        input[type="checkbox"]:checked::before {
          transform: scale(1);
          background-color: #fff;
        }
        input[type="checkbox"]:checked {
          transform: scale(1);
          background-color: #004EEF;
        }
        p{
          margin: 0;
          font-weight: 500;
          font-size: 14px;
          line-height: 170.3%;
          color: #31425A;
          margin-left: 17px;
        }
      }
    }
  }
}

//popper options
.popper{
  position: relative !important;
  transform: unset !important;
  .options{
    position: absolute !important;
    top: 0;
    left: 0;
    background: #fff;
    box-shadow: 0px 12px 34px -12px rgba(0, 0, 0, 0.16);
    border-radius: 14px;
    width: 100%;
    
    div div{
      display: flex;
      &:hover{
        background: #b1aaaa;
        border-radius: 14px;
      }
      img{
        margin-left: 18px;
      }
      span{
        padding: 24px 18px;
        
      }
    }
  }
  .overflow{
    height: 200px;
    overflow-y: scroll;
    
  }
}

//label animation
.label-animation{
  position: relative;
  .password-style{
    display: flex;
    align-items: center;
    .input{
      padding-left: 18px;
      @media #{$mobile}{
        padding-left: 20px;
      }
    }
    a{
      img{
        position: absolute;
        top: 50%;
        right: 23.5px;
        transform: translateY(-50%);
        z-index: 10;
        cursor: pointer;
        @media #{$mobile}{
          transform: translateY(-90%);
        }
      }
    }
  }
}
.input{
  border: 0; 
  padding: 4px 0; 
  border-bottom: 1px solid #ccc; 
  background-color: transparent;
}

.input ~ .focus-border{
  position: absolute; 
  bottom: 0; 
  left: 50%; 
  width: 0; 
  height: 2px; 
  background-color: #004EEF; 
  transition: 0.4s;
  
}
.input:focus ~ .focus-border{
  width: 90%; 
  transition: 0.4s;
  left: 5%;
}
.input ~ label{
  position: absolute; 
  left: 18px; 
  top: 50%;
  transform: translateY(-50%); 
  color: #aaa; 
  transition: 0.3s; 
  z-index: 1; 
  letter-spacing: 0.5px;
  @media #{$mobile}{
    transform: translateY(-50%);
  }
}
.input:focus ~ label,
.input:not(:placeholder-shown).input:not(:focus) ~ label {
  top: 13px; 
  font-size: 12px; 
  color: #76879E; 
  transition: 0.3s;
}


//select style
.select{
  position: relative;
	display: flex;
	background-color: transparent;
	overflow: hidden;
	width: 100%;
  font-weight: 500;
  color: #76879E;
  font-family: 'DM Sans';
	select {
		-webkit-appearance: none;
		-moz-appearance: none;
		-ms-appearance: none;
		appearance: none;
		outline: 0;
		box-shadow: none;
		border: 0 !important;
		background-image: none;
		background-color: transparent;
		width: 318px;
		position: relative;
		z-index: 15;
    font-size: 16px;
    font-weight: 400 !important;
		cursor: pointer;
	}
	&:after{
		content: url('../assets/Vector.svg');
		position: absolute;
		top: 50%;
		right: 26px;
		color: black;
		transform: translateY(-50%);
		z-index: 20;
	}
}

//validation
.error{
  border: 1px solid red !important;
  color: red;
  text-align: left;
}
.error-message{
  color: red;
}

//notification
.notification{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 888px;
  height: auto;
  background: #FFFFFF;
  box-shadow: 0px 40px 60px -33px rgba(0, 0, 0, 0.04);
  border-radius: 25px;
  .notification-content{
    padding: 224px 179px;
    .img{
      background: #17BA87;
      display: inline-block;
      width: 108px;
      height: 108px;
      box-shadow: 0px 17px 31px rgba(44, 202, 117, 0.25);
      border-radius: 66px;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 0 auto;
      margin-bottom: 32px;
    }
    img{
      width: 26.71px;
      height: 17px;
    }
    h3{
      font-weight: 500;
      font-size: 60px;
      line-height: 66px;
      margin-bottom: 14px !important;
      color: #333333;
    }
    p{
      font-weight: 400;
      font-size: 18px;
      line-height:32px;
      text-align: center;
      color: #76879E;
    }
  }
}

//transition animation
.show-enter-from {
  opacity: 0;
  transform: scale(0);
  position: absolute;
  top: 10%;
  left: 10%;
  transition: 0.5s all ease;
}

.show-enter-to {
  opacity: 1;
  transform: scale(1);
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: 0.5s all ease;
}

.show-leave-to {
  opacity: 0;
  transition: 0.5s all ease;
}
.active-item {
  background-color: red;
}

.margin-bottom-0{
  @media #{$mobile}{
    margin-bottom: 0px !important;
  }
}
</style>
