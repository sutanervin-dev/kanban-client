<template>
  <div class="container d-flex justify-content-center">
        <div class="card border-light mt-5" style="width: 18rem;">
            <div class="card-body border-0 rounded no-boder">
                <form @submit.prevent="updateTask">
                    <h1>Edit Task</h1>
                    <div class="form-group">
                        <label for="title">Title</label>
                        <input type="text" class="form-control" v-model="dataToEdit.title" aria-describedby="emailHelp">
                    </div>

                    <div class="form-group">
                        <label for="category">Select category:</label>
                        <select class="form-control" v-model="dataToEdit.category">
                            <option>backlog</option>
                            <option>product</option>
                            <option>development</option>
                            <option>done</option>
                        </select>
                    </div>
                    <button type="submit" class="btn btn-primary">Submit</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props: ['dataToEdit', 'reloadTask'],
    data(){
      return{
          title: this.dataToEdit.title,
          category: this.dataToEdit.category
        }
    },
    methods: {
        updateTask(){
            console.log('asdasd')
            console.log(this.dataToEdit.id)
            axios({
                method: 'PUT',
                url: `http://localhost:3002/tasks/${this.dataToEdit.id}`,
                data: {
                    title: this.dataToEdit.title,
                    category: this.dataToEdit.category
                },
                headers: {
                    access_token: localStorage.access_token
                }
            }).then(({ data }) => {
                console.log(data, 'updated data')
                this.reloadTask()
            }).catch(err => {
                console.log(err)
            })
        }
    }
    // computed: {
    //     dataTitle(){
    //         let title = this.dataToEdit.title
    //         return title
    //     },
    //     dataCategory(){
    //         let category = this.dataToEdit.category
    //         return category
    //     },
    //     dataId(){
    //         let id = this.dataToEdit.id
    //         return id
    //     }
    // }
}
</script>

<style>

</style>