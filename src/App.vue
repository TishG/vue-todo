<template>
  <div id="app">
    <Header title="Vue Todo" />
    <div class="main">
      <Form @add-todo="addTodo" />
      <Todos :todos="todos" @del-todo="deleteTodo" />
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header";
import Todos from "./components/Todos";
import Form from "./components/Form";
import Footer from "./components/Footer";

export default {
  name: "app",
  components: {
    Header,
    Todos,
    Form,
    Footer
  },
  data() {
    return {
      todos: [
        { title: "Play Tennis", completed: false, id: 1 },
        { title: "Grocery Shopping", completed: false, id: 2 },
        {
          title: "Complete Vue project",
          completed: false,
          id: 3
        }
      ]
    };
  },
  methods: {
    deleteTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      todo.visible = !todo.visible;
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-image: url("https://images.unsplash.com/photo-1498354136128-58f790194fa7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=800&q=60");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  font-family: "Raleway", sans-serif;
}

#app {
  background-color: rgba(135, 206, 250, 0.3);
  display: -webkit-box; /* OLD - iOS 6-, Safari 3.1-6 */
  display: -moz-box; /* OLD - Firefox 19- (buggy but mostly works) */
  display: -ms-flexbox; /* TWEENER - IE 10 */
  display: -webkit-flex; /* NEW - Chrome */
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
  width: 100%;
  margin: auto;
}

.main {
  margin: 50px auto;
}
@media screen and (max-width: 700px) {
  .main {
    width: 90%;
  }
}

@media screen and (min-width: 701px) and (max-width: 1200px) {
  .main {
    width: 70%;
  }
}

@media screen and (min-width: 1201px) {
  .main {
    width: 50%;
  }
}
</style>
