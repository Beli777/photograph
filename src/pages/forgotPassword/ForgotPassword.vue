<template>
  <div class="wrapper" id="home-wrapper">
      <h1>Welcome to <span>Photogram</span></h1>
      <section class="login">
          <div class="row">
            <div class="col-md-6 col-md-push-3">

                <div class="panel panel-default">
                    <div class="panel-heading"><strong>Forgot Your Password</strong></div>
                        <div class="panel-body">
                            <form v-on:submit.prevent="handleForgotFormSubmit()">
                                <div class="form-group">
                                    <label>Email address</label>
                                    <input class="form-control" placeholder="Enter your email adress" type="text" v-model='email'>
                                </div>

                                <button class="btn btn-primary">Send</button>
                            </form>
                        </div>
                    </div>
                </div>

            </div>
          </div>
      </section>
  </div>
</template>

<script>
import {forgotPassword} from '../../config'
import toastr from 'toastr'
export default {
    data(){
        return{
            email: ''
        }
    },
    methods:{
        handleForgotFormSubmit (){
            const postData = {
                email: this.email
            }
            this.$http.post(forgotPassword, postData)
            .then(response => {
                if (response.status === 200){
                    toastr.success('Email was sent to you, please confirm !')
                    setTimeout(
                        this.$router.push({name: 'resetPassword'})
                    ,3000);
                    // this.$http.get(apiDomain, {headers: getHeader()})
                    // this.$router.push({name: 'dashboard'})
                    // .then(response => {
                    //     window.localStorage.setItem('authUser', JSON.stringify(authUser))
                    //     this.$router.push({name: 'dashboard'})
                    // })
                }
            }, (response) => {
              toastr.warning('Email was not found in database !')
        });
    }
}
}
</script>

<style lang="scss" scoped>
    @import '../../assets/css/bootstrap.css';

    .row{
        margin: 3% auto;
    }
    .fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}
    h1{
        text-align: center;
        margin-top: 10rem;
        span{
            color: orange;
        }
    }
    .login{
        transition: .5s all ease-in;
    }
    .nav-tabs{
        background-color:#158cba;
        border-bottom: 1px solid #158cba;
        a{
            border:0;
            margin: 0;
            cursor: pointer;
            color: #fff;
                padding: 15px 25px;
            &:hover{
                padding: 15px 25px;
                border-radius: 0;
                color: #000;
            }
        }
        .active{
                background-color:orange;
                    color: #fff;
                    border-radius:0;
        }
    }
</style>
