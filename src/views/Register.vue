<template>
  <div class="container d-flex justify-content-center">
        <div class="card border-light mt-5" style="width: 18rem;">
            <div class="card-body border-0 rounded no-boder">
                <form @submit.prevent="register">
                    <div class="form-group">
                        <label for="email">Email address</label>
                        <input type="email" class="form-control" v-model="email" aria-describedby="emailHelp">
                    </div>
                    <div class="form-group">
                        <label for="password">Password</label>
                        <input type="password" class="form-control" v-model="password">
                    </div>
                    <!-- <button type="submit" class="btn btn-primary" @click.prevent="changeRegister(false)">Register</button> -->
                    <button type="submit" class="btn btn-primary">Register</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props: ['changeRegister'],
    data(){
            return{
                email: '',
                password: ''
            }
        },
        methods: {
            register(){
                axios({
                    method: 'POST',
                    url: 'http://localhost:3002/register',
                    data: {
                        email: this.email,
                        password: this.password
                    }
                }).then(response => {
                    this.changeRegister(false)
                }).catch(err => {
                    console.log(err) //sementara
                })
            }
        }
}
</script>

<style>

</style>