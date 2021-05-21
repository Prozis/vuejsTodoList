<template>
  <div>
    <ul>
      <TodoItem
        v-for="(todo, index) in todos"
        v-bind:todo="todo"
        v-bind:key="todo.id"
        v-bind:index="index"
        v-on:removeTodo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
  name: "TodoList",
  props: ['todos'],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      this.$emit('removeTodo', id)
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style: none;
  padding: 0 50px;

  margin: 30px auto;
  text-align: left;
  max-width: 800px;
}

a {
  color: #42b983;
}
</style>