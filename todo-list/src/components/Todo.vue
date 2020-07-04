<template>
  <!--
    The styles are provided by the Semantic UI framework
  -->
  <div class="ui centered card">

    <div class="content" v-show="!isEditing">
      <div class="header">
        {{ todo.title }}
      </div>
      <div class="meta">
        {{ todo.project }}
      </div>
      <div class="extra content">
        <span class="right floated edit icon" v-on:click="showForm">
          <i class="edit icon"></i>
        </span>
        <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
          <i class="trash icon"></i>
        </span>
      </div>
    </div>

    <!--
      Check isEditing, if true enables the edit todo form
    -->
    <div class="content" v-show="isEditing">
      <div class="ui form">
        <div class="field">
          <label>Title</label>
          <input type="text" v-model="todo.title">
        </div>
        <div class="field">
          <label>Project</label>
          <input type="text" v-model="todo.project">
        </div>
        <div class="ui two button attached buttons">
          <button class="ui basic blue button" v-on:click="hideForm">
            Save
          </button>
        </div>
      </div>
    </div>

    <!--
      Check for isEditing and done status using Javascrip operators
      inside the 'v-show'
    -->
    <div class='ui bottom attached green basic button' v-show="!isEditing && todo.done" v-on:click="changeTodoStatus(todo)" disabled>
      Completed
    </div>
    <div class='ui bottom attached red basic button' v-show="!isEditing && !todo.done" v-on:click="changeTodoStatus(todo)">
      Pending
    </div>

  </div>
</template>

<script type="text/javascript">
export default {
  props: ['todo'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    showForm () {
      this.isEditing = true
    },

    hideForm () {
      this.isEditing = false
    },

    deleteTodo (todo) {
      /*
        Emit a 'delete-todo' event to TodoList Parent
      */
      this.$emit('delete-todo', todo)
    },

    changeTodoStatus (todo) {
      this.$emit('change-todo-status', todo)
    }
  }
}
</script>

<style scoped>
</style>
