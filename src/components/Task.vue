<template>
    <div class="card mb-2" style="width: 28rem;">
        <div class="card-body">
            <p class="card-text">{{ task.title}}</p>
            <p class="card-text text-muted">{{ task.createdAt }}</p>
            <a class="card-link" @click="editTask(task.id)">Edit</a>
            <!-- <div class="dropdown">
                <a class="dropdown-toggle" href="#" id="dropdownMenuLink"
                    data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    Dropdown link
                </a>

                <div class="dropdown-menu" aria-labelledby="dropdownMenuLink">
                    <a class="dropdown-item" href="#">Action</a>
                    <a class="dropdown-item" href="#">Another action</a>
                    <a class="dropdown-item" href="#">Something else here</a>
                </div>
            </div> -->
            <a class="card-link" @click="deleteTask(task.id)">Delete</a>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        props: ['task', 'reloadTask', 'showEdit', 'assignDataEdit'],
        methods: {
            editTask(id) {
                axios({
                    method: 'GET',
                    url: `http://localhost:3002/tasks/${id}`,
                    headers: {
                        access_token: localStorage.access_token
                    }
                }).then(({
                    data
                }) => {
                    console.log(data, 'edit data')
                    this.assignDataEdit(data)
                    this.showEdit(true)
                }).catch(err => {
                    console.log(err)
                })
            },
            deleteTask(id) {
                axios({
                    method: 'DELETE',
                    url: `http://localhost:3002/tasks/${id}`,
                    headers: {
                        access_token: localStorage.access_token
                    }
                }).then(({
                    data
                }) => {
                    this.reloadTask()
                }).catch(err => {
                    console.log(err)
                })
            }
        }
    }
</script>

<style>

</style>