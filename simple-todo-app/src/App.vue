<template>
  <div id="app">
    <h3>{{ title }}</h3>
    <form @submit.prevent="addTodo" >
      <label for="newTodo">New Todo</label>
      <input type="text" name="newTodo" id="newTodo" v-model="newTodo">
      <button type="submit" name="button">Add Todo</button>
    </form>
    <button @click="allDone">All Done</button>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.isDone">
        <span :class="{ done: todo.isDone }" >{{ todo.title }}</span>
        <button @click="removeTodo(todo)">Remove Todo</button>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'App',
  methods: {
    addTodo(){
      if (this.newTodo.length > 0){
        this.todos.push({
        title: this.newTodo,
        isDone: false
      });
      this.newTodo = '';
      }
      else{
        alert("Input box cannot be empty.");
      }
    },
    removeTodo(todo){
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    allDone() {
      if(this.todos.length > 0){
          this.todos.forEach(todo => {
          todo.isDone = true;
        })
      }
      else{
        alert("No Todos to mark as checked!");
      }
    }
  },
  data() {
    return {
      title: 'Simple Todo App Using Vue Js',
      newTodo:  '',
      todos: []
    }
  }
}
</script>

<style>
.done{
  text-decoration: line-through;
}

ul {
  display: inline-block;
}

ul li {
  display: list-item;
  text-emphasis: none;
}
</style>
