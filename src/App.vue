<template>
  <div class="wrapper" id="home-wrapper">
      <h1>Welcome to <span>Photogram</span></h1>
      <section class="login">
          <div class="row">
            <div class="col-md-6 col-md-push-3">
                <div class="panel panel-default">
                    <div class="panel-heading"><strong>Login</strong></div>
                        <div class="panel-body">
                            <form v-on:submit.prevent="handleLoginFormSubmit()">
                                <div class="form-group">
                                    <label>Email address</label>
                                    <input class="form-control" placeholder="Enter your email adress" type="text" v-model='email'>
                                </div>

                                <div class="form-group">
                                    <label>Password</label>
                                    <input class="form-control" placeholder="Enter your password" type="password" v-model='password'>
                                </div>

                                <button class="btn btn-primary">Login</button>
                            </form>


                        </div>
                    </div>

                    <div class="panel panel-default">
                        <div class="panel-heading"><strong>Login</strong></div>
                            <div class="panel-body">
                                <form v-on:submit.prevent="handleRegisterFormSubmit()">
                                    <div class="form-group">
                                        <label>Email</label>
                                        <input class="form-control" placeholder="Enter your email adress" type="text" v-model='registeremail'>
                                    </div>

                                    <div class="form-group">
                                        <label>Username</label>
                                        <input class="form-control" placeholder="Enter your Username" type="text" v-model='username'>
                                    </div>

                                    <div class="form-group">
                                        <label>Username</label>
                                        <input class="form-control" placeholder="Enter your Name" type="text" v-model='name'>
                                    </div>

                                    <div class="form-group">
                                        <label>Password</label>
                                        <input class="form-control" placeholder="Enter your password" type="password" v-model='registerpassword'>
                                    </div>

                                    <button class="btn btn-primary">Register</button>
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
import {apiDomain, getHeader, userUrl, registerUrl} from './config'
import toastr from 'toastr'
export default {
    data(){
        return{
            email: '',
            password:'',
            username: '',
            name: '',
            registeremail: '',
            registerpassword: ''
        }
    },
    methods:{
        handleLoginFormSubmit (){
            const postData = {
                email: this.email,
                password: this.password
            }
            const authUser = {}
            this.$http.post(apiDomain, postData)
            .then(response => {
                if (response.status === 200){
                    authUser.access_token = response.body.token
                    window.localStorage.setItem('authUser', JSON.stringify(authUser))
                    this.$router.push({name: 'dashboard'})
                    // this.$http.get(apiDomain, {headers: getHeader()})
                    // this.$router.push({name: 'dashboard'})
                    // .then(response => {
                    //     window.localStorage.setItem('authUser', JSON.stringify(authUser))
                    //     this.$router.push({name: 'dashboard'})
                    // })
                }
            }, (response) => {
              toastr.warning('Username or password is incorrect, please try again !')
        });
    },
    handleRegisterFormSubmit (){
        const registerData = {
            email: this.registeremail,
            username: this.username,
            name: this.name,
            password: this.registerpassword
        }
        this.$http.post(registerUrl, registerData)
        .then(response => {
            if (response.status >= 200){
                console.log(response)
            }
        }, (response) => {
            if (response.error != ''){
          toastr.error('Duplicated email, please try something else !')
            }
    });
}
}
}
</script>

<style lang="scss" scoped>
    @import './assets/css/bootstrap.css';

    .row{
        margin: 3% auto;
    }
    h1{
        text-align: center;
        margin-top: 10rem;
        span{
            color: orange;
        }
    }
    .register{
        margin-top:-30px;
        float:right;
    }
</style>
