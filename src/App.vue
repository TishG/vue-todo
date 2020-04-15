<template>
  <div id="app" :style="{ backgroundColor: appOverlayColor }">
    <Message
      @clear-todos="clearTodos"
      @del-todo="delTodo"
      @close-message="closeMessage"
      :displayMessage="displayMessage"
    />
    <MyHeader
      :title="title"
      :showMenu="showMenu"
      :showToggler="showToggler"
      @open-menu="openMenu"
      @close-menu="closeMenu"
      @show-completed="showCompleted"
      @show-uncompleted="showUncompleted"
      @show-all="showAll"
      @open-message="openMessage"
    />
    <MyAd />
    <div class="main">
      <Form @add-todo="addTodo" />
      <p class="no-Todos-message" v-if="noTodos !== null">{{ noTodos }}</p>
      <Todos
        :todos="todos"
        :showAllTodos="showAllTodos"
        :filteredTodos="filteredTodos"
        :showFilteredTodos="showFilteredTodos"
        @del-todo-message="deleteTodoMessage"
        @mark-complete="markComplete"
        @edit-todo="editTodo"
        @edited-todo="editedTodo"
        @toggle-shown="toggleShown"
      />
    </div>
    <MyFooter :title="title" />
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader";
import MyAd from "./components/MyAd";
import Form from "./components/Form";
import Todos from "./components/Todos";
import MyFooter from "./components/MyFooter";
import Message from "./components/Message";
import moment from "moment";

export default {
  name: "app",
  components: {
    MyHeader,
    MyAd,
    Form,
    Todos,
    MyFooter,
    Message
  },
  data() {
    return {
      title: "Noetify",
      todos: [],
      filteredTodos: [],
      showAllTodos: true,
      showFilteredTodos: false,
      list: "all to dos",
      appOverlayColor: "rgba(135, 206, 250, 0.3)",
      displayMessage: {
        m1: "Are you sure you want to delete this list?",
        m2: "Deletion is permanent and irreversible.",
        show: false,
        next: null
      },
      showMenu: false,
      showToggler: true,
      noTodos: null
    };
  },
  methods: {
    addTodo(newTodo) {
      const ago = moment().format("lll");
      newTodo.posted.ago = ago;
      newTodo.posted.date = moment().format("ll");
      const newTodos = [newTodo, ...this.todos];
      this.todos = newTodos;
    },
    clearTodos() {
      this.todos = [];
      this.showAllTodos = true;
      this.showFilteredTodos = false;
      this.appOverlayColor = "rgba(135, 206, 250, 0.3)";
      this.displayMessage.show = false;
      this.showMenu = !this.showMenu;
      this.showToggler = true;
    },
    closeMenu() {
      this.showToggler = !this.showToggler;
      this.showMenu = !this.showMenu;
    },
    closeMessage() {
      this.displayMessage.show = false;
      this.appOverlayColor = "rgba(135, 206, 250, 0.3)";
      this.showMenu = false;
      this.showToggler = true;
      // this.displayMessage.m1 = "Are you sure you want to delete this list?";
    },
    delTodo() {
      const newTodos = this.todos.filter(
        todo => todo.id !== this.displayMessage.next
      );
      this.todos = newTodos;
      this.closeMessage();
      this.displayMessage.next = null;
    },
    deleteTodoMessage(id) {
      this.openMessage();
      const todo = this.todos.find(todo => todo.id === id);
      const len = todo.title.length > 40 ? "...." : "";
      this.displayMessage.m1 =
        'Are you sure you want to delete "' +
        todo.title.trim().substring(0, 40) +
        len +
        '" from the list?"';
      this.displayMessage.next = id;
    },
    editedTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo.title.trim() === "")
        return (todo.editError = "Please submit text");
      else {
        todo.editError = "";
        todo.isEditing = !todo.isEditing;
        localStorage.setItem("todos", JSON.stringify(this.todos));
        this.todos = JSON.parse(localStorage.getItem("todos"));
      }
    },
    editTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      todo.isEditing = !todo.isEditing;
    },
    markComplete(id) {
      const newTodos = this.todos.map(todo =>
        todo.id === id
          ? (todo = { ...todo, completed: !todo.completed })
          : { ...todo }
      );
      this.todos = newTodos;
    },
    openMenu() {
      this.showToggler = !this.showToggler;
      this.showMenu = !this.showMenu;
    },
    openMessage() {
      this.appOverlayColor = "rgba(0, 0, 0, 0.5)";
      this.displayMessage.m1 = "Are you sure you want to delete this list?";
      this.displayMessage.show = true;
      if (this.todos.length === 0) {
        this.displayMessage.m1 = 'Action Omitted: List is already empty.';
        this.displayMessage.m2 = "";
        return false;
      }
    },
    showAll() {
      this.showAllTodos = true;
      this.showFilteredTodos = false;
      this.list = "all to dos";
    },
    showCompleted() {
      this.filteredTodos = this.todos.filter(todo => todo.completed);
      this.showAllTodos = false;
      this.showFilteredTodos = true;
      this.list = "completed to dos";
    },
    showUncompleted() {
      this.filteredTodos = this.todos.filter(todo => !todo.completed);
      this.showAllTodos = false;
      this.showFilteredTodos = true;
      this.list = "uncompleted to dos";
    },
    toggleShown(id) {
      const todo = this.todos.find(todo => todo.id === id);
      todo.visibility === "visible"
        ? (todo.visibility = "hidden")
        : (todo.visibility = "visible");
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.todos = JSON.parse(localStorage.getItem("todos"));
    }
  },
  beforeMount() {
    if (localStorage.getItem("todos")) {
      this.todos = JSON.parse(localStorage.getItem("todos"));
    }
  },
  beforeUpdate() {
    localStorage.setItem("todos", JSON.stringify(this.todos));
    if (this.todos.length === 0 && this.list === "all to dos") {
      this.noTodos = "There are no to dos.";
    } else if (
      this.filteredTodos.length === 0 &&
      this.list === "completed to dos"
    ) {
      this.noTodos = "There are no completed to dos.";
    } else if (
      this.filteredTodos.length === 0 &&
      this.list === "uncompleted to dos"
    ) {
      this.noTodos = "There are no uncompleted to dos.";
    } else {
      this.noTodos = null;
    }
  },
  mounted() {
    if (!localStorage.getItem("todos")) {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    }
    if (this.todos.length === 0 && this.list === "all to dos") {
      this.noTodos = "There are no to dos.";
    } else if (
      this.filteredTodos.length === 0 &&
      this.list === "completed to dos"
    ) {
      this.noTodos = "There are no completed to dos.";
    } else if (
      this.filteredTodos.length === 0 &&
      this.list === "uncompleted to dos"
    ) {
      this.noTodos = "There are no uncompleted to dos.";
    } else {
      this.noTodos = null;
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
  background-attachment: fixed;
  background-origin: border-box;
  font-family: "Raleway", sans-serif;
  min-width: 300px;
  min-height: 100%;
}

body::-webkit-scrollbar {
  background-color: rgb(0, 0, 0, 0.7);
}

body::-webkit-scrollbar-thumb {
  background-color: rgba(135, 206, 250, 0.5);
}

.menu::-webkit-scrollbar {
  background-color: rgba(0, 0, 0);
}

.menu::-webkit-scrollbar-thumb {
  background-color: rgba(255, 255, 255, 0.1);
}

#app {
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
  margin: auto;
}

.main {
  margin: 5px auto;
  width: 90%;
}

.list-type {
  margin-left: 10px;
  margin-bottom: 5px;
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

.no-Todos-message {
  color: blue;
  padding-top: 1%;
}
</style>
