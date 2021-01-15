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
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

    export default {
    props: ['dataIsLogin', 'changeLogin', 'changeRegister'],
        data(){
            return{
                email: '',
                password: ''
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
                    console.log(response);
                    localStorage.access_token = response.data.access_token
                    this.changeLogin(true)
                }).catch(err => {
                    console.log(err) //sementara
                })
            }
        }
    }
</script>

<style>

</style>