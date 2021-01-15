<template>
    <div>
        <div class="container-fluid mt-2">
            <div class="row">
                <Board v-for="category in categories" 
                :key="category.id" 
                :dataCategory="category" 
                :dataTask="tasks"
                :reloadTask="fetchTask"
                :showEdit="changeShowEdit"
                :assignDataEdit="assignDataEdit"
                ></Board>
            </div>
        </div>
</template>

<script>
    import Board from '../components/Board'
    import Task from '../components/Task'
    import axios from 'axios'

    export default {
        props: ['fetchCategory', 'fetchTask', 'categories', 'tasks', 'changeShowEdit','assignDataEdit'],
        data() {
            return {
                boards: []
            }
        },
        components: {
            Task,
            Board
        },
        created() {
            this.fetchCategory()
        }
    }
</script>

<style>

</style>