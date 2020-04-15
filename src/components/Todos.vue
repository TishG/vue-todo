<template>
  <div class="todos">
    <transition-group
      enter-active-class="animated fadeIn"
      leave-active-class="animated fadeOut"
      tag="div"
    >
      <div v-for="todo in todos" :key="todo.id" v-show="showAllTodos">
        <TodoItem
          :todo="todo"
          @del-todo-message="$emit('del-todo-message', todo.id)"
          @mark-complete="$emit('mark-complete', todo.id)"
          @edit-todo="$emit('edit-todo', todo.id)"
          @edited-todo="$emit('edited-todo', todo.id)"
          @toggle-shown="$emit('toggle-shown', todo.id)"
        />
      </div>
    </transition-group>
    <div v-for="todo in filteredTodos" :key="todo.id" v-show="showFilteredTodos">
      <TodoItem :todo="todo" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos", "showAllTodos", "filteredTodos", "showFilteredTodos"]
};
</script>

<style scoped>
.todos {
  margin: auto;
  display: flex;
  flex-direction: column;
}
</style>


