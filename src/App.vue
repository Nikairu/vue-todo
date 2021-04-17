<template>
  <div class="--todo_main">
    <md-field>
      <md-input
        class="--todo_input"
        v-model="currentTodo"
        @keydown.enter="addTodo"
        placeholder="Add a todo"
      ></md-input>
    </md-field>
    <ul class="todos">
      <li
        v-for="todo in todos"
        :key="todo.id"
        v-bind:id="todo.id"
        v-bind:class="{ completed: todo.completed }"
      >
        <button @click="removeTodo(todo)" class="--styled_button">
          <md-icon>cancel</md-icon>
        </button>
        <button @click="editingTodo(todo)" class="--styled_button">
          <md-icon>create</md-icon>
        </button>
        <input type="checkbox" v-model="todo.completed" />
        <span class=".todo-name" v-show="!todo.editing">{{ todo.label }}</span>

        <input
          class=".todo-name"
          v-show="todo.editing"
          @keydown.enter="todo.editing = !todo.editing"
          v-model="todo.label"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
    };
  },
  methods: {
    editingTodo(todo) {
      todo.editing = !todo.editing;
    },
    addTodo() {
      if (this.currentTodo === "") {
        //do nothing if field is empty
        return;
      }
      this.todos.push({
        id: "todo-" + this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false,
        edit: "",
      });
      this.currentTodo = "";
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
ul {
  list-style-type: none;
}
.--todo_input {
  padding-left: 10px;
  padding-right: 10px;
}

.--todo_main {
  max-width: 800px;
  margin: auto;
}

.--styled_button {
  background-color: unset;
  border: unset;
}

.todos {
  width: 100%;
  margin: auto;
}

.completed {
  text-decoration: line-through;
}
li[id^="todo"] * {
  vertical-align: middle;
}
</style>
