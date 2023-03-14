<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: {},
      isEditing: false,
      indexEdit: 0,
      buttonText: 'Add'
    }
  },
  methods: {
    addTodo: function (form) {
      form.preventDefault()
      if (this.newTodo.title === ' ' || this.newTodo.title === '' || this.newTodo.title === undefined)
        return
      if (!this.isEditing) {
        let date = new Date()
        date = date.toLocaleString('fr-FR')
        this.newTodo = {
          title: this.newTodo.title,
          createdAt: date,
          done: false
        }
        this.todos.push(this.newTodo)
        this.newTodo = {}
      }
      if (this.isEditing) {
        this.todos[this.indexEdit].title = this.newTodo.title
        this.newTodo = {}
        this.buttonText = 'Add'
      }
    },
    changeTodo: function (todo) {
      if (todo.done)
        todo.done = false
      else todo.done = true
    },
    updateTodo: function (index) {
      const todo = this.todos[index]
      this.newTodo.title = todo.title
      this.isEditing = true
      this.indexEdit = index
      this.buttonText = 'Edit'
    },
    deleteTodo: function (todo) {
      const listTodos = this.todos.filter(element => element != todo)
      this.todos = listTodos
    },
    deleteAll: function () {
      this.todos = []
    },
    deleteDone: function () {
      const listTodos = this.todos.filter(element => element.done === false)
      this.todos = listTodos
    }
  }
}
</script>

<template>
  <div class="card">
    <form @submit="addTodo">
      <input v-model="newTodo.title" placeholder="Add Task">
      <button type="submit">{{ buttonText }}</button>
    </form>
    <div class="list">
      <div class="todo" v-for="(todo, index) in todos">
        <p :class="{ done: todo.done }">{{ todo.title }}</p>
        <button @click="changeTodo(todo)">Done</button>
        <button @click="updateTodo(index)">Update</button>
        <button @click="deleteTodo(todo)">Delete</button>
      </div>
    </div>
    <button @click="deleteAll">Delete all tasks</button>
    <button @click="deleteDone">Delete all tasks done</button>
  </div>
</template>
