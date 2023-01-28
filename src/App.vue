<template>
  <div>
    <h1>Todo App</h1>
    <div v-for="todo in todos" :key="todo.id" :todo="todo" class="todo">
      <span
        :class="[todo.isCompleted ? 'has-line-through' : '']"
        class="todo-name"
      >
        👉 {{ todo.name }}
      </span>

      <button @click="onComplete(todo)" class="complete-btn">
        {{ todo.isCompleted ? 'Undo' : 'Complete' }}
      </button>
      <button @click="onDelete(todo.id)" class="dlt-btn">Delete</button>
    </div>
    <div>
      <input type="text" v-model="todo" />
      <button @click="addTodos" :disabled="!todo" class="add-btn">
        Add Todo
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      todo: '',
      todos: [
        {
          id: 1,
          name: 'Buy an abd',
          isCompleted: false,
        },
      ],
    };
  },
  methods: {
    addTodos() {
      console.log('added');
      console.log(this.todos.length + 1);

      this.todos.push({
        id: this.todos.length + 1,
        name: this.todo,
        isCompleted: false,
      });
      this.todo = '';
    },
    onComplete(todo) {
      console.log('completed');
      todo.isCompleted = !todo.isCompleted;
    },
    onDelete(id) {
      console.log('deleted');
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px 80px;
  padding-bottom: 60px;
  border: solid 2px gray;
}
.has-line-through {
  text-decoration: line-through;
}
.todo {
  margin: 10px 0 10px 0;
}
.todo-name {
  margin-right: 20px;
}
.complete-btn {
  cursor: pointer;
  background-color: green;
  border: solid 1px;
  border-radius: 5px;
  padding: 8px 12px;
  color: white;
}
.complete-btn:hover {
  background-color: white;
  color: green;
}
.dlt-btn {
  cursor: pointer;
  background-color: red;
  border: solid 1px;
  border-radius: 5px;
  padding: 8px 12px;
  color: white;
}
.dlt-btn:hover {
  background-color: white;
  color: red;
}
</style>
