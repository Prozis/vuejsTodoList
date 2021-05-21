<template>
  <form @submit.prevent="onsubmit">
    <input type="text" v-model="title">
    <button type="submit">Добавить</button>
  </form>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: ''
    }
  },
  methods: {
    onsubmit() {
      if(this.title.trim()) {
        const newTodo = {
            id: Date.now(),
            title: this.title,
            completed: false
        }
        this.$emit('addTodo', newTodo)
        this.title = ''
      }
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
    justify-content: center;
  }
  input {
    min-width: 400px;
    max-width: 600px;
    border-radius: 5px;
  }
  button {
    border-radius: 5px;
  }
</style>