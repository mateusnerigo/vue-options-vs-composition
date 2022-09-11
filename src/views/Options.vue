<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>You have {{ todosCount }} TODOs!</h3>

    <div>
      <input
        v-model="newTodoName"
        @keyup.enter="addTodo"
        placeholder="Add a TODO"
        type="text"
      >
    </div>

    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Options',

  data() {
    return {
      newTodoName: '',
      todos: [],
      swearwords: ['fart', 'butt hair', 'willy']
    }
  },

  computed: {
    todosCount() { return this.todos.length; },
  },

  methods: {
    addTodo() {
      if (this.newTodoName != '') {
        const newTodo = {
          id: Date.now(),
          name: this.newTodoName
        };

        this.todos.push(newTodo);
        this.newTodoName = '';
      }
    },

    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  },

  watch: {
    newTodoName(newValue) {
      if (this.swearwords.includes(newValue.toLowerCase())) {
        this.newTodoName = '';
        alert(`You must NEVER say ${newValue}!`);
      }
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}

li {
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}

li span {
  flex-grow: 1;
}

li button {
  border-radius: 0;
  border: none;
}
</style>
