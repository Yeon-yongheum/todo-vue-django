<template>
  <div class="todo-list">
        <ul>
            <li v-for="todo in todos" :key="todo.id.todoId">
                {{ todo.user }} : {{ todo.title }}
            </li>
        </ul>
  </div>
</template>

<script>
export default {
    name: 'TodoList',
    props:{
        todos:{
            type: Array,
            required: true
        }
    }
}
</script>

<style>

</style>