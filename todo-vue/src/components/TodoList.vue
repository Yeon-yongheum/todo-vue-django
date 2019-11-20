<template>
  <div class="todo-list">
        <ul>
            <li v-for="todo in todos" :key="todo.id">
                <input @change="updateTodo(todo)" type="checkbox" v-model="todo.is_completed">
                {{ todo.user }} : {{ todo.title }}
                <button @click="deleteTodo(todo)">x</button>
            </li>
        </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'TodoList',
    props:{
        todos:{
            type: Array,
            required: true
        }
    },
    methods:{ 
        deleteTodo(todo){
            this.$session.start()
            const token = this.$session.get('jwt')
            const options = {
                headers:{
                Authorization: `JWT ${token}` // JWT 다음에 공백있음
                }
            }
            axios.delete(`http://127.0.0.1:8000/api/v1/todos/${todo.id}/`, options)
            .then(response =>{
                console.log(response)
                // const target = this.todos.find( el => {
                //     return el === todo
                // })
                const idx = this.todos.indexOf(todo)
                if (idx > -1){
                    this.todos.splice(idx, 1)
                }
            })
            .catch(error => {
                console.log(error)
            })
        },

        updateTodo(todo){
            this.$session.start()
            const token = this.$session.get('jwt')
            const options = {
                headers:{
                Authorization: `JWT ${token}` // JWT 다음에 공백있음
                }
            }
            // const data = {
            //     'id' : todo.id,
            //     'used_id' : todo.used_id,
            //     'title' : todo.title,
            //     'is_completed' : todo.is_completed
            // }
            axios.put(`http://127.0.0.1:8000/api/v1/todos/${todo.id}/`, todo, options)
            .then(response =>{
                console.log(response)
            })
            .catch(error => {
                console.log(error)
            })
        }
    }
}
</script>

<style>

</style>