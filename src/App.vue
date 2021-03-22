<template>
  <div>hehe
    <input v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a todo">
    <ul class="todos">
      <li  v-for="todo in todos" :key="todo.id" v-bind:class="{completed: todo.completed}">
        <input type='checkbox' v-model="todo.completed">
        {{ todo.label }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, label: this.currentTodo, completed: false});
      this.currentTodo = '';
    }
  }
};
</script>

<style>
.completed{
text-decoration: line-through;
}

</style>