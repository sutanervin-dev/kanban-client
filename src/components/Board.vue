<template>
    <div class="col-sm-3 mt-2">
        <div class="card " style="height: 700px;">
            <div class="card-header">
                {{ dataCategory.category }}
            </div>

            <div v-if="filterTask.length > 0" class="card-body overflow-auto">
                <div class="row">
                    <Task v-for="task in filterTask" :key="task.id" 
                    :task="task" 
                    :reloadTask="reloadTask"
                    :showEdit="showEdit"
                    :assignDataEdit="assignDataEdit"
                    ></Task>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Task from '../components/Task'
    export default {
        props: ['dataCategory', 'dataTask', 'reloadTask', 'showEdit', 'assignDataEdit'],
        components: {
            Task
        },
        computed: {
            filterTask() {
                return this.dataTask.filter(e => e.category === this.dataCategory.category)
            }
        },
        created() {
            // console.log(this.dataTask, 'test datatask')
            // console.log(this.dataCategory, 'test datacategory')
        }
    }
</script>

<style>

</style>