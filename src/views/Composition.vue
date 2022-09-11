<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>You have {{ todosCount }} TODOs!</h3>

    <div>
      <input
        v-model="data.newTodoName"
        @keyup.enter="addTodo"
        placeholder="Add a TODO"
        type="text"
      >
    </div>

    <div>
      <ul>
        <li v-for="(todo, index) in data.todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import {
  reactive,
  computed,
  watch,
} from 'vue';

export default {
  name: 'Composition',

  setup() {
    const swearwords = ['fart', 'butt hair', 'willy'];

    // reactive
    let data = reactive({
      newTodoName: '',
      todos: []
    })


    // computed
    let todosCount = computed( () => data.todos.length )


    // functions
    function addTodo() {
      if (newTodoName.value != '') {
        const newTodo = {
          id: Date.now(),
          name: data.newTodoName
        };

        data.todos.push(newTodo);
        data.newTodoName = '';
      }
    }

    function deleteTodo(index) {
      data.todos.splice(index, 1);
    }
    // functions


    // watchers
    watch(data, ( newValue ) => {
      if (swearwords.includes(newValue.newTodoName.toLowerCase())) {
        alert(`You must NEVER say ${newValue.newTodoName}!!`);
        data.newTodoName = '';
      }
    })

    return {
      // reactive
      data,

      // computed
      todosCount,

      // functions
      addTodo,
      deleteTodo
    };
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
