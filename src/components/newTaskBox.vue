<script>
import axios from 'axios'

export default {
    name: 'newTaskBox',

    data() {
        return {
        tasks: null,
        new_task: '',
        apiNewTask: 'http://localhost:80/PHP/php-todo-list-json/newTask.php',
        apiGetTask: 'http://localhost:80/PHP/php-todo-list-json/getTask.php',

        }
    },
    methods: {
        add_task() {
            const data = {
                new_task: this.new_task
            }
            axios.post(this.apiNewTask, data,
                {
                    headers: { 'Content-Type': 'multipart/form-data' }
                }).then(response => {
                    console.log(response);
                    this.tasks = response.data
                })
                .catch(error => {
                    console.error(error.message);
                })
            this.new_task = "";
        },
    },
    mounted() {
        axios
        .get(this.apiGetTask)
        .then(response => {
            console.log(response);
            this.tasks = response.data
        })
        .catch(error => {
            console.error(error.message);
    })
  },
}
</script>
<template>
    <div class="my_container new_task p-2">
        <input type="text" v-model="new_task" @keyup.enter="add_task()" placeholder="Inserisci un nuovo elemento...">
        <button type="submit" @click="add_task()" class="btn btn-outline-light mx-5">Inserisci</button>
    </div>
</template>


<style lang="scss" scoped></style>