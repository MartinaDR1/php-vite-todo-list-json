<script>
import axios from 'axios'
import newTaskBox from './newTaskBox.vue'

export default {
    name:'appMain',

    data() {
        return {
        tasks: null,
        apiGetTask: 'http://localhost:80/PHP/php-todo-list-json/getTask.php',
        apiDeleteTask: 'http://localhost:80/PHP/php-todo-list-json/deleteTask.php',
        apiDoneTask:'http://localhost:80/PHP/php-todo-list-json/doneTask.php',
        new_task: '',
        }
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
    methods: {
        deleteItem(index) {
        //this.tasks.splice(i, 1);

        const data = {
            index
        }
        axios.post(this.apiDeleteTask, data,
            {
            headers: { 'Content-Type': 'multipart/form-data' }
            }).then(response => {
            console.log(response);
            this.tasks = response.data
            })
            .catch(error => {
            console.error(error.message);
            })
        },
        doneItem(index) {
        //console.log(index)
        //this.tasks[index].done = !this.tasks[index].done

        const data = {
            index
        }
        axios.post(this.apiDoneTask, data,
            {
            headers: { 'Content-Type': 'multipart/form-data' }
            }).then(response => {
            console.log(response);
            this.tasks = response.data
            })
            .catch(error => {
            console.error(error.message);
            })
        }
    },
    components:{
        newTaskBox
    }
}
</script>
<template>
    <div class="my_container">
      <ul class="text-black list-unstyled fs-2 p-2">
        <li v-for="(task, index) in tasks" class="border-bottom d-flex justify-content-between">
          <span :class="task.done ? 'done' : ''" @click="doneItem(index)">{{ task.task }}</span>

          <div class="btn">
            <button class="btn btn-outline-success my-2 mx-2" @click="doneItem(index)"><i
                class="fa-solid fa-check fa-2xs"></i></button>
            <button class="btn btn-outline-danger my-2" @click="deleteItem(index)"><i
                class="fa-solid fa-xmark fa-2xs"></i></button>
          </div>
        </li>
      </ul>
    </div>
    <newTaskBox></newTaskBox>
</template>


<style lang="scss" scoped></style>