<!--
  The .vue files can only have one 'template' and 'script' block
  but can have a lot of 'style' blocks. Hipocrisy ~gus
-->
<template>
  <div>
    <p>Completed Tasks: {{ todos.filter(todo => {return todo.done === true}).length }}</p>
    <p>Pending Tasks: {{ todos.filter(todo => {return todo.done === false}).length }}</p>

    <todo v-for="todo in todos"
      v-bind:todo="todo"
      v-bind:key="todo.id"
      v-on:delete-todo="deleteTodo"
      v-on:change-todo-status="changeTodoStatus"
    ></todo>

  </div>
</template>

<script type="text/javascript">
import Todo from './Todo'

export default {
  props: ['todos'],
  components: {
    Todo
  },
  methods: {
    deleteTodo (todo) {
      /*
        Delete the specified Todo by splicing the todos array
      */
      const todoIndex = this.todos.indexOf(todo)

      this.todos.splice(todoIndex, 1)
    },

    changeTodoStatus (todo) {
      const todoIndex = this.todos.indexOf(todo)

      todo.done
        ? this.todos[todoIndex].done = false
        : this.todos[todoIndex].done = true
    }
  }
}
</script>

<style scoped>
</style>
