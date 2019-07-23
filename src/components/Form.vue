<template>
  <div class="todo-form">
    <form @submit.prevent="addTodo">
      <input type="text" v-model="title" name="title" placeholder="What's the agenda?..." />
      <button class="submit">Add</button>
    </form>
  </div>
</template>

<script>
import uuid from "uuid";
export default {
  name: "Form",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo() {
      if (this.title.trim() === "") return;
      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false
      };
      //send up to parent component
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style>
@media screen and (max-width: 700px) {
  form input {
    width: 85%;
  }
  form button {
    width: 15%;
  }
}

@media screen and (min-width: 700px) {
  form input {
    width: 90%;
  }
  form button {
    width: 10%;
  }
}
form input {
  padding: 16px;
  /* width: 90%; */
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  border: 1px solid rgba(5, 103, 149, 1);
  font-size: 1.05rem;
}

form input:focus,
form button:focus {
  outline: none;
}

form button {
  /* width: 10%; */
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 16px 0px;
  background-color: rgba(0, 0, 0, 1);
  color: rgba(255, 255, 255, 1);
  border: 1px solid rgba(0, 0, 0, 1);
  transition: background-color 1s ease-in-out;
  font-size: 1.05rem;
}

form button:hover {
  background-color: rgba(0, 0, 0, 0.8);
  border: 1px solid rgba(0, 0, 0, 0.8);
  cursor: pointer;
}

form button:active {
  transform: scale(0.98);
}
</style>
