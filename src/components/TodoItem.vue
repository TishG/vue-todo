<template>
  <div class="todo-item">
    <div class="left-aligned" :style="{visibility: todo.visibility}">
      <div class="top">
        <div class="checkbox" @click="$emit('mark-complete', todo.id)" v-show="!todo.isEditing">
          <i class="fa fa-square" v-show="!todo.completed"></i>
          <i class="fa fa-check-square" v-show="todo.completed"></i>
          <span :class="{'is-completed':todo.completed}">{{todo.title}}</span>
        </div>
        <form @submit.prevent="$emit('edited-todo', todo.id)" v-show="todo.isEditing">
          <input type="text" v-model="todo.title" name="title" />
          <div
            class="edit-error"
            v-if="todo.title == '' && todo.editError !== ''"
          >{{todo.editError}}</div>
        </form>
      </div>
      <div class="bottom">
        <small
          v-if="todo.posted.ago && todo.posted.date"
        >{{ todo.posted.ago | moment("from", "now")}} ({{todo.posted.date}})</small>
      </div>
    </div>
    <div class="right-aligned">
      <div class="item-button">
        <div class="hide-show" @click="$emit('toggle-shown', todo.id)">
          <i class="fas fa-eye-slash hide" v-show="todo.visibility === 'hidden'"></i>
          <i class="fas fa-eye show" v-show="todo.visibility === 'visible'"></i>
        </div>
        <i
          class="fas fa-pen edit"
          @click="$emit('edit-todo', todo.id)"
          v-show="todo.isEditing !== undefined && (todo.visibility === 'visible' || todo.visibility == undefined)"
        ></i>
        <i
          class="far fa-trash-alt delete"
          @click="$emit('del-todo-message', todo.id)"
          v-show="todo.visibility === 'visible' || todo.visibility == undefined"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "TodoItem",
  props: ["todo", "showTodo"],
  computed: {
    now() {
      return moment().format();
    }
  }
};
</script>

<style scoped>
.todo-item {
  min-height: 3em;
  box-sizing: border-box;
  margin: auto;
  opacity: 1;
  cursor: pointer;
  display: flex;
  display: -ms-flexbox;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(5, 103, 149, 0.4);
  color: rgba(0, 0, 0, 1);
  font-weight: 600;
  padding: 6px 12px;
  border-bottom: 1px solid rgba(5, 103, 149, 1);
}

.item-button {
  display: flex;
  flex-direction: row;
}

input {
  width: inherit;
}

.todo-item form {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 90%;
}

@media screen and (min-width: 701px) {
  .todo-item form {
    width: 100%;
  }
}

.is-completed {
  text-decoration: line-through;
  color: rgb(105, 105, 105);
}

.display-none {
  display: none;
}

.display {
  display: block;
}

.fa-square,
.fa-check-square {
  margin-right: 5px;
}

.left-aligned {
  display: flex;
  flex-direction: column;
}

.fa-square {
  color: rgba(0, 0, 0, 1);
  transition: color 0.2s ease-in-out;
}

.fa-square:hover {
  color: rgba(0, 0, 0, 0.5);
}

.fa-check-square {
  color: rgb(105, 105, 105);
}

.delete,
.edit {
  color: rgba(0, 0, 0, 0.8);
  transition: all 0.5s ease-in-out;
}

.delete:hover,
.edit:hover {
  color: rgba(0, 0, 0, 1);
  transform: scale(1.2);
}

.show {
  color: rgba(0, 0, 0, 0.8);
}

.show:hover {
  color: rgba(0, 0, 0, 0.8);
}

.hide {
  color: rgba(105, 105, 105, 0.8);
}

.hide:hover {
  color: rgba(105, 105, 105, 1);
}

p {
  white-space: nowrap;
}

.delete,
.edit,
.hide,
.show {
  margin: 0 0.2rem;
}

.edit-error {
  width: inherit;
  background-color: rgb(178, 34, 34);
  font-weight: 100;
  color: rgb(255, 255, 255);
}

.checkbox {
  word-wrap: break-word;
}

form {
  display: flex;
}

input {
  height: 40px;
}
</style>
