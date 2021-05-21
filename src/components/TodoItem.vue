<template>
<li>
  <span v-bind:class="{
    done: todo.completed
  }">
    <input type="checkbox" v-on:change="todo.completed= !todo.completed">
    <strong>{{ index + 1 }}</strong>
    <!--    вывод заголовка, обработанного фильтром-->
    {{ todo.title | uppercase}}
  </span>
  <button class="remove"
    v-on:click="$emit('removeTodo', todo.id)"
  >&times;</button>
</li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
  input {
    margin-right: 1rem;
  }
  li {
    border: 1px solid black;
    border-radius: .5rem;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin: 1rem;
  }
  .remove {
    background: #b0afaf;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
  }

  .remove:hover {
    background: red;

  }
  .done {
    text-decoration: line-through;
  }
</style>