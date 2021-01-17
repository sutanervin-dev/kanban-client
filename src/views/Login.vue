<template>
    <div class="container d-flex justify-content-center">
        <div class="card border-light mt-5" style="width: 18rem;">
            <div class="card-body border-0 rounded no-boder">
                <form @submit.prevent="login">
                    <div class="form-group">
                        <label for="email">Email address</label>
                        <input type="email" class="form-control" v-model="email" aria-describedby="emailHelp">
                    </div>
                    <div class="form-group">
                        <label for="password">Password</label>
                        <input type="password" class="form-control" v-model="password">
                    </div>
                    <button type="submit" class="btn btn-primary">Submit</button>
                    <button type="submit" class="btn btn-primary" @click.prevent="changeRegister(true)">register</button>
                    <GoogleLogin :params="params" :renderParams="renderParams" :onSuccess="onSuccess"></GoogleLogin>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import GoogleLogin from 'vue-google-login'

    export default {
    props: ['dataIsLogin', 'changeLogin', 'changeRegister'],
    components: {
        GoogleLogin
    },
        data(){
            return{
                email: '',
                password: '',
                params: {
                    client_id: '633618943220-bvn060o0j8gg98venuti0sfdpsmrq1nf.apps.googleusercontent.com'
                },
                renderParams: {
                    width: 250,
                    height: 50,
                    longtitle: true
                }
            }
        },
        methods: {
            login(){
                axios({
                    method: 'POST',
                    url: 'http://localhost:3002/login',
                    data: {
                        email: this.email,
                        password: this.password
                    }
                }).then(response => {
                    // console.log(response, 'login biasa');
                    localStorage.access_token = response.data.access_token
                    this.changeLogin(true)
                }).catch(err => {
                    console.log(err) //sementara
                })
            },
            onSuccess(googleUser){
                    const id_token = googleUser.getAuthResponse().id_token
                    axios({
                        method: 'POST',
                        url: 'http://localhost:3002/googleLogin',
                        data: {
                            id_token
                        }
                    }).then((response) => {
                        // console.log(response, 'response glogin')
                        localStorage.access_token = response.data.access_token
                        this.changeLogin(true)
                    }).catch (err => {
                        console.log(err)
                    })
                }
        }
    }
</script>

<style>

</style>