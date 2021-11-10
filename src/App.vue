<template>
  <div id="app">
    <nav class="navbar navbar-transparent navbar-fixed-top" role="navigation">
      <div class="logo-left col-2">
        <img src="./assets/logo1.png" class="logo" alt="logo1" />
      </div>
      <div class="logo-right col-2">
        <img src="./assets/logo2.png" class="logo" alt="logo2" />
      </div>
    </nav>
    <img class="main" src="./assets/bg.png" alt="main" />
    <img class="suna_vector" src="./assets/suna_vector.png" alt="suna_vector" />
    <div class="footer">
      <div class="footer_form">
        <div class="logo-left col-2">
          <img src="./assets/logo1.png" class="logo" alt="logo1" />
        </div>
        <div class="col-md-12 col-8 mail_sender">
          <form
            class="form-inline"
            role="form"
            @submit="checkForm"
            novalidate="true"
          >
            <label class="form-group lbl_input" for="exampleInputEmail2"
              >Get in Touch</label
            >
            <div class="form-group">
              <input
                type="email"
                class="form-control transparent"
                id="email"
                required="required"
                v-model="email"
                label="Email*"
              />
            </div>
            <button type="submit" class="btn btn-fill form-group submit">
              Submit
            </button>
          </form>
        </div>
        <div class="logo-right col-2">
          <img src="./assets/logo2.png" class="logo" alt="logo2" />
        </div>
      </div>
      <div class="copyright_info">
        <p class="owner_address">
          VQualis Limited &nbsp;&nbsp;
          Grand Industrial Building, Office 7/F &nbsp;&nbsp;
          159-165 Wo Yi Hop Road &nbsp;&nbsp;
          Kwai Chung, Hongkong &nbsp;&nbsp;
          Company No: 2948312 &nbsp;&nbsp;
        </p>
        <p class="copyright">
          © Copyright. VQualis Limited  2020. All rights reserved
        </p>
      </div>
    </div>
  </div>
  <div id="snackbar"></div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      errors: [],
      touch_txt: "Get in Touch",
      email: "",
    };
  },
  methods: {
    checkForm: function (e) {
      var x = document.getElementById("snackbar");
      
      e.preventDefault();
      this.errors = [];
      if (!this.email) {
        this.errors.push("Email required.");
        x.className = "show warning";
        x.innerHTML = 'Email is required!';
        setTimeout(function(){ x.className = x.className.replace("show warning", ""); }, 2900);
      } else if (!this.validEmail(this.email)) {
        this.errors.push("Valid email required.");
        x.className = "show warning";
        x.innerHTML = 'Valid Email is required!';
        setTimeout(function(){ x.className = x.className.replace("show warning", ""); }, 2900);
      }

      if (!this.errors.length) {
        const email = { email: this.email };
        console.log(email);
        axios
          .post("/sendMail", email)
          // .post("http://localhost:4000/sendMail", email)
          .then((response) => {
            if (response.statusText == "OK") console.log("aaaaa");
            x.className = "show success";
            x.innerHTML = 'Success! Mail Sent.';
            setTimeout(function(){ x.className = x.className.replace("show success", ""); }, 2900);
          })
          .catch((e) => {
            console.log(e);
            x.className = "show error";
            x.innerHTML = 'Error happened!';
            setTimeout(function(){ x.className = x.className.replace("show error", ""); }, 2900);
          });
      } else {
        console.log(this.errors);
      }
      
      this.email = "";
    },
    validEmail: function (email) {
      var re =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
  },
};
</script>

<style>
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  .footer {
    position: absolute !important;
    bottom: 0 !important;
    width: 100%;
    color: white;
    text-align: center !important;
    background: #192f5d !important;
    padding: 10px;
  }
  .footer_form {    
    min-height: 65px;
    display: flex;
    align-content: center;
    justify-content: center;
  }
  .main {
    height: auto;
    min-height: 100%;
    min-width: 100%;
    position: absolute;
    width: auto;
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
  .navbar {
    padding: 10px;
    position: relative;
    border: 0 none;
    transition: all 0.4s;
    -webkit-transition: all 0.4s;
    font-size: 16px;
    background: #192f5d !important;
  }
  .navbar-fixed-top {
    top: 0;
    z-index: 30;
  }
  @media (min-width: 1080px) {
    .copyright_info {
      display: flex;
      justify-content: space-around;
    }
  }
  @media (min-width: 768px) {
    .navbar {
      display: none;
    }
    .footer .logo {
      width: 100px;
      height: auto;
      display: block;
    }
    .form-inline .form-group {
      display: inline-block;
      margin-bottom: 0;
      vertical-align: middle;
    }
    .form-inline .form-control {
      display: inline-block;
    }
    .submit {
      margin-left: 5px;
    }
    .lbl_input {
      margin-right: 15px;
    }
  }
  @media (max-width: 768px) {
    .form-group {
      width: 100%;
    }
    .col-md-12 {
      width: 100%;
    }
    .navbar {
      display: flex;
    }
    .footer .logo {
      display: none;
    }
    .copyright_info {
      display: block;
    }
    .navbar .logo-left,
    .navbar .logo-right {
      width: 12%;
      min-width: 70px;
    }
    .navbar .logo {
      width: 100%;
      height: auto;
    }
    .submit {
      margin-left: 0;
    }
    .lbl_input {
      margin-right: 0;
    }
  }
  .mail_sender {
    margin: auto;
  }
  .lbl_input {
    font-size: 24px;
    font-weight: bold;
  }
  .form-group {
    margin-bottom: 15px;
  }
  .submit {
    background-color: red;
    color: white;
    padding: 6px 12px;
    line-height: 1.428571429;
    white-space: nowrap;
    vertical-align: middle;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    border-radius: 4 px;
    user-select: none;
  }
  .submit:hover {
    background-color: #f00d;
    color: #e9d16f;
  }
  #email {
    min-width: 270px;
  }
  .form-control {
    display: block;
    width: 100%;
    height: 34px;
    padding: 6px 12px;
    font-size: 14px;
    line-height: 1.428571429;
    color: #555555;
    background-color: #ffffff;
    background-image: none;
    border: 1px solid #cccccc;
    border-radius: 4px;
    -webkit-box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%);
    box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%);
    -webkit-transition: border-color ease-in-out 0.15s,
      box-shadow ease-in-out 0.15s;
    transition: border-color ease-in-out 0.15s, box-shadow ease-in-out 0.15s;
  }

  .logo-left {
    left: 0;
  }
  .navbar .logo-right {
    right: 10px;
    position: absolute;
  }
  .btn {
    display: inline-block;
    padding: 6px 12px;
    margin-bottom: 0;
    font-size: 14px;
    font-weight: normal;
    line-height: 1.428571429;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    border-radius: 4px;
  }

  .btn:focus {
    outline: thin dotted #333;
    outline: 5px auto -webkit-focus-ring-color;
    outline-offset: -2px;
  }
  *,
  *:before,
  *:after {
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }

  body {
    font-size: 14px;
    margin: 0;
    line-height: 1.428571429;
    box-sizing: border-box;
    overflow: hidden;
  }

  .suna_vector {
    min-width: 100%;
    width: auto;
    height: auto;
    max-height: 37%;
    position: fixed;
    left: 50%;
    transform: translate(-50%);
    bottom: 25px;
    z-index: 9;
  }
  .footer .footer_form> div {
    z-index: 10;
  }
  .copyright_info p {
    margin-bottom: 0 !important;
  }
  .copyright_info {
    font-size: 12px;
    text-align: center;
  }
  .copyright {
    margin-left: 20px;
    color: yellow;
    font-weight: bold;
  }
  .owner_address {
    color: white;
  }
  #snackbar {
    visibility: hidden;
    min-width: 250px;
    background-color: #2196f3;
    color: #fff;
    text-align: center;
    border-radius: 2px;
    padding: 16px;
    position: fixed;
    z-index: 1;
    right: 30px;
    top: 30px;
    font-size: 17px;
    border-radius: 5px;
    box-shadow: 0 3px 5px -1px rgb(0 0 0 / 40%), 0 6px 10px 0 rgb(0 0 0 / 25%), 0 1px 18px 0 rgb(0 0 0 / 15%);
  }
  #snackbar.warning {
    background-color: darkorange;
  }
  #snackbar.success {
    background-color: #2196f3;
  }
  #snackbar.error {
    background-color: crimson;
  }
  #snackbar.show {
    visibility: visible;
    -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
    animation: fadein 0.5s, fadeout 0.5s 2.5s;
  }

  @-webkit-keyframes fadein {
    from {top: -30px; opacity: 0;} 
    to {top: 30px; opacity: 1;}
  }

  @keyframes fadein {
    from {top: -30px; opacity: 0;}
    to {top: 30px; opacity: 1;}
  }

  @-webkit-keyframes fadeout {
    from {top: 30px; opacity: 1;} 
    to {top: -30px; opacity: 0;}
  }

  @keyframes fadeout {
    from {top: 30px; opacity: 1;}
    to {top: -30px; opacity: 0;}
  }
</style>
