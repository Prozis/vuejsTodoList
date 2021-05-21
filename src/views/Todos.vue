<template>
  <div>
    <div class="top">
      <h2>Todo list</h2>
      <router-link to="/">Home page</router-link>
    </div>

    <AddTodo
        @addTodo = "addTodo"
    />

    <select v-model="filter">
      <option value="all" selected>All</option>
      <option value="completed">completed</option>
      <option value="not-completed">not completed</option>
    </select>
    <Loader
        v-if="loading"
    />

    <TodoList
        v-bind:todos="filteredTodos"
        @removeTodo="removeTodo"
        v-else-if="filteredTodos.length"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>

import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all',
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  computed: {
    filteredTodos() {
      if(this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }
      if(this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
      return this.todos
    }
  },
  methods: {
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !==id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  mounted() {
    // получение рандомных значений для теста
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loading = false
          }, 500)
        })
  }
}
</script>

<style>
.top {
  margin-bottom: 40px;
}
</style>

