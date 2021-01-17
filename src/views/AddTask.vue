<template>
    <div class="container d-flex justify-content-center">
        <div class="card border-light mt-5" style="width: 18rem;">
            <div class="card-body border-0 rounded no-boder">
                <form @submit.prevent="addTask">
                    <h1>Add Task</h1>
                    <div class="form-group">
                        <label for="title">Title</label>
                        <input type="text" class="form-control" v-model="task.title" aria-describedby="emailHelp">
                    </div>

                    <div class="form-group">
                        <label for="category">Select category:</label>
                        <select class="form-control" v-model="task.category">
                            <option>backlog</option>
                            <option>product</option>
                            <option>development</option>
                            <option>done</option>
                        </select>
                    </div>

                    <button type="submit" class="btn btn-primary" @click.prevent="changeShowAdd(false)">Cancel</button>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

    export default {
        props: ['fetchTask', 'changeShowAdd'],
        data(){
            return{
                task: {
                    title: '',
                    category: ''
                }
            }
        },
        methods: {
            addTask(){
                axios({
                    method: 'POST',
                    url: 'http://localhost:3002/tasks',
                    data: this.task,
                    headers: {
                        access_token: localStorage.access_token
                    }
                }).then(({ data }) => {
                    this.fetchTask()
                    this.changeShowAdd(false)
                }).catch(err => {
                    console.log(err)
                })
            }
        }
    }
</script>

<style>

</style>