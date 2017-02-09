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
                </div>
            </div>
          </div>
      </section>
  </div>
</template>

<script>
import {apiDomain, getHeader, userUrl} from './config'
import toastr from 'toastr'
export default {
    data(){
        return{
            email: '',
            password:''
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
                    console.log(response)
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
</style>
