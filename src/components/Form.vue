<template>
  <div class="todo-form">
    <form @submit.prevent="addTodo">
      <input type="text" v-model="title" name="title" />
      <button class="submit">add</button>
    </form>
    <div class="form-error" v-if="error != '' && title == ''">{{error}}</div>
  </div>
</template>

<script>
import uuid from "uuid";
export default {
  name: "Form",
  data() {
    return {
      title: "",
      error: ""
    };
  },
  methods: {
    addTodo() {
      if (this.title.trim() === "")
        return (this.error = "You must submit text");
      else {
        this.error = "";
        const newTodo = {
          id: uuid.v4(),
          title: this.title,
          completed: false,
          isEditing: false,
          editError: "",
          visibility: "visible",
          posted: {
            ago: null,
            date: null
          }
        };
        //send up to parent component
        this.$emit("add-todo", newTodo);
        this.title = "";
      }
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

::placeholder,
webkit-input-placeholder {
  color: rgba(169, 169, 169, 0.7);
}

form input {
  padding: 12px;
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
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding: 12px 0px;
  background-color: rgb(50, 50, 50);
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

.form-error {
  background-color: rgb(178, 34, 34);
  color: rgb(255, 255, 255);
  padding: 5px;
}
</style>
