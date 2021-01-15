<template>
  <div>
      <Navbar v-if="isLogin" 
      :dataIsLogin="isLogin" 
      :changeShowAdd="changeShowAdd"
      :isLogin="isLogin"
      :changeIsLogin="changeIsLogin"
      ></Navbar>

      <Login v-if="!isLogin" 
      :dataIsLogin="isLogin" 
      :changeLogin="changeIsLogin"
      :changeRegister="changeRegister"
      ></Login>

      <Register v-if="isRegister && !isLogin"
      :changeRegister="changeRegister"
      ></Register>

      <AddTask v-if="isLogin && showAdd" 
      :fetchTask="fetchTask"
      :changeShowAdd="changeShowAdd"
      ></AddTask>
      
      <EditTask v-if="isLogin && showEdit"
      :fetchTask="fetchTask"
      :changeShowEdit="changeShowEdit"
      :dataToEdit="dataToEdit"
      ></EditTask>

      <Home v-if="isLogin && !showAdd" 
      :fetchTask="fetchTask" 
      :tasks="tasks" 
      :fetchCategory="fetchCategory" 
      :categories="categories"
      :changeShowEdit="changeShowEdit"
      :assignDataEdit="assignDataEdit"
      ></Home>
  </div>
</template>

<script>
import Navbar from './components/Navbar'

import Login from './views/Login'
import Register from './views/Register'
import Home from './views/Home'
import AddTask from './views/addTask'
import EditTask from './views/EditTask'

import axios from 'axios'

export default {
    data(){
        return {
            isLogin: false,
            isRegister: false,
            showRegister: false,
            showAdd: false,
            showEdit: false,
            tasks: [],
            categories: [],
            dataToEdit: {}
        }
    },
    //register component
    components: {
        Navbar,
        Login,
        Home,
        AddTask,
        EditTask,
        Register
    },
    methods: {
        changeIsLogin(value){
            this.isLogin = value
        },
        changeRegister(value){
            this.isRegister = value
        },
        changeShowAdd(value){
            this.showAdd = value
        },
        changeShowEdit(value){
            this.showEdit = value
        },
        assignDataEdit(value){
            this.dataToEdit = value
            console.log(this.dataToEdit, '<< data to edit')
        },
        fetchTask() {
            axios({
                method: 'GET',
                url: 'http://localhost:3002/tasks',
                headers: {
                    access_token: localStorage.access_token
                }
            }).then(({ data }) => {
                console.log(data, 'fetch task')
                this.tasks = data
            }).catch(err => {
                console.log(err)
            })
        },
        fetchCategory() {
            axios({
                method: 'GET',
                url: 'http://localhost:3002/category',
                headers: {
                    access_token: localStorage.access_token
                }
            }).then(({ data }) => {
                // console.log(data)
                this.categories = data
            }).catch(err => {
                console.log(err)
            })
        }
    },
    created(){
        if(localStorage.access_token){
            this.isLogin = true
            this.fetchTask()
        }else{
            this.isLogin = false
        }


    }
}
</script>

<style>

</style>