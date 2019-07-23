<template>
  <div class="todo-item">
    <div class="left-aligned">
      <div class="checkbox" @click="markComplete">
        <i class="fa fa-square" v-show="!todo.completed"></i>
        <i class="fa fa-check-square" v-show="todo.completed"></i>
        <span :class="{'is-completed':todo.completed}">{{todo.title}}</span>
      </div>
    </div>
    <div class="right-aligned">
      <i class="fa fa-minus" @click="$emit('del-todo', todo.id)"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todo-item {
  margin: auto;
  opacity: 1;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgba(5, 103, 149, 0.4);
  color: rgba(0, 0, 0, 1);
  font-weight: 600;
  padding: 15px;
  border-bottom: 1px solid rgba(5, 103, 149, 1);
  transition: opacity 2s ease-in-out;
  animation: fadeIn 2s forwards;
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
  margin-right: 15px;
}

.left-aligned {
  display: flex;
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

.fa-minus {
  color: rgba(0, 0, 0, 0.8);
  transition: all 0.5s ease-in-out;
}

.fa-minus:hover {
  color: rgba(0, 0, 0, 1);
  transform: scale(1.2);
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}
/* 
.fade-out {
  animation: fadeOut 2s forwards;
}

@keyframes fadeOut {
  from {
    opacity: 1;
  }

  to {
    opacity: 0;
  }
} */
</style>
