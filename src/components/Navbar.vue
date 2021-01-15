<template>
    <div class="container-fluid m-0 p-0 shadow">
        <nav class="navbar navbar-dark bg-primary">
            <a class="navbar-brand">Kanban App</a>
            <form class="form-inline">
                <a class="btn btn-outline-light my-2 my-sm-0 mr-2"
                @click.prevent="changeShowAdd(true)"
                >Add Task</a>
                <button id="btn-logout" class="btn btn-outline-light my-2 my-sm-0" type="submit" @click="logout">logout</button>
            </form>
        </nav>
    </div>
</template>

<script>
    export default {
        props: ['dataIsLogin', 'changeShowAdd', 'changeIsLogin'],
        methods: {
            logout(){
                localStorage.clear()
                this.changeIsLogin(false)
            }
        }
    }
</script>

<style>

</style>