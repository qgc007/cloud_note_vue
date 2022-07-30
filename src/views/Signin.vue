<template>
  <div class="container top-0 position-sticky z-index-sticky">
    <div class="row">
      <div class="col-12">
<!--        <navbar-->
<!--          isBlur="blur  border-radius-lg my-3 py-2 start-0 end-0 mx-4 shadow"-->
<!--          v-bind:darkMode="true"-->
<!--          isBtn="bg-gradient-success"-->
<!--        />-->
      </div>
    </div>
  </div>
  <main class="mt-0 main-content">
    <section>

      <note-alert :color="msgStatus" icon="ni ni-check-bold" dismissible :message="message" v-if="showMsg">
        <strong>Dark!</strong> This is a dismissible alert!
      </note-alert>
      <div class="page-header min-vh-100">
        <div class="container">
          <div class="row">
            <div class="mx-auto col-xl-4 col-lg-5 col-md-7 d-flex flex-column mx-lg-0">
              <div class="card card-plain">
                <div class="pb-0 card-header text-start">
                  <h4 class="font-weight-bolder">Sign In</h4>
                  <p class="mb-0">Enter your email and password to sign in</p>
                </div>
                <div class="card-body">
                  <form role="form" class="was-validated" id="login-form">
                    <div class="mb-3">
                      <note-input type="email" placeholder="Email" name="email" size="lg" v-model:value="email" id="email" isRequired
                                  data-bs-toggle="tooltip" title="请输入您已注册邮箱"/>
                    </div>
                    <div class="mb-3">
                      <note-input type="password" placeholder="Password" name="password" size="lg"  v-model:value="pwd" isRequired
                                  minlength="6" maxlength="20" data-bs-toggle="tooltip" title="请输入密码6-15位"/>
                    </div>
                    <note-switch id="rememberMe">Remember me</note-switch>
                  </form>
                  <div class="text-center">
                    <note-button @click="signIn"
                                 class="mt-4"
                                 variant="gradient"
                                 color="success"
                                 fullWidth
                                 size="lg"
                    >Sign in</note-button>
                  </div>
                </div>
                <div class="px-1 pt-0 text-center card-footer px-lg-2">
                  <p class="mx-auto mb-4 text-sm">
                    Don't have an account?
                    <a
                      href="/signup"
                      class="text-success text-gradient font-weight-bold"
                    >Sign up</a>
                  </p>
                </div>
              </div>
            </div>
            <div
              class="top-0 my-auto text-center col-6 d-lg-flex d-none h-100 pe-0 position-absolute end-0 justify-content-center flex-column"
            >
              <div
                class="position-relative bg-gradient-primary h-100 m-3 px-7 border-radius-lg d-flex flex-column justify-content-center overflow-hidden"
                style="background-image: url('https://raw.githubusercontent.com/creativetimofficial/public-assets/master/argon-dashboard-pro/assets/img/signin-ill.jpg');
          background-size: cover;"
              >
                <span class="mask bg-gradient-success opacity-6"></span>
                <h4
                  class="mt-5 text-white font-weight-bolder position-relative"
                >"Attention is the new currency"</h4>
                <p
                  class="text-white position-relative"
                >The more effortless the writing looks, the more effort the writer actually put into the process.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
// import Navbar from "@/examples/PageLayout/Navbar.vue";
import NoteInput from "@/components/NoteInput.vue";
import NoteSwitch from "@/components/NoteSwitch.vue";
import NoteButton from "@/components/NoteButton.vue";
const body = document.getElementsByTagName("body")[0];
import  global from '../global';
import NoteAlert from "@/components/NoteAlert.vue";
export default {
  name: "signin",
  data(){
    return{
      email:"",
      pwd:"",
      message:"登录成功",
      showMsg:false,
      msgStatus:"success"
    }
  },
  components: {
    // Navbar,
    NoteInput,
    NoteSwitch,
    NoteButton,
    NoteAlert
  },
  methods:{
    signIn(){
      let form= document.querySelectorAll("#login-form")[0];
      if(form.checkValidity() === false){
        return;
      }
      global.ajax.post(global.SignInURL,{"umail":this.email,"upwd":this.pwd}).then(response =>{
        this.showMsg=true;
        if(response.data.result === "OK") {
          this.message="info:    登录成功";
          this.msgStatus="success";
          setTimeout( ()=>this.$router.push("/dashboard-default"),500)
        }
        else{
          this.message="warning:   密码或者用户名错误！";
          this.msgStatus="warning";
        }
      }).catch(err=>{
        this.message="fatal:   服务器错误！";
        this.msgStatus="danger";
        console.log("err" + err);
      })
    }
  },
  created() {
    this.$store.state.hideConfigButton = true;
    this.$store.state.showNavbar = false;
    this.$store.state.showSidenav = false;
    this.$store.state.showFooter = false;
    body.classList.remove("bg-gray-100");
  },
  beforeUnmount() {
    this.$store.state.hideConfigButton = false;
    this.$store.state.showNavbar = true;
    this.$store.state.showSidenav = true;
    this.$store.state.showFooter = true;
    body.classList.add("bg-gray-100");
  },
};
</script>