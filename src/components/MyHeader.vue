<template>
  <div class="header">
    <h1>{{title}}</h1>
    <div class="toggle-menu">
      <!-- toggle menu button -->
      <i class="fa fa-bars open-menu" v-show="showToggler" @click="$emit('open-menu')"></i>
      <!-- displayed menu -->
      <transition name="fade">
        <div class="menu" v-show="showMenu">
          <div class="exit">
            <h3>{{title}}</h3>
            <i class="fa fa-bars close-menu" @click="$emit('close-menu')"></i>
          </div>
          <div class="menu-items first" @click="$emit('show-completed')">Completed</div>
          <div class="menu-items" @click="$emit('show-uncompleted')">Uncompleted</div>
          <div class="menu-items" @click="$emit('show-all')">All</div>
          <div class="menu-items" @click="$emit('open-message')">Clear list</div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "myHeader",
  props: ["title", "showMenu", "showToggler"]
};
</script>

<style scoped>
.header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
h1 {
  padding: 20px 30px;
  height: 70px;
}

.toggle-menu {
  padding: 20px 30px;
}

.open-menu,
.close-menu {
  font-size: 25px;
  transition: 0.4s ease-in-out;
}

.open-menu:hover {
  color: rgba(0, 0, 0, 0.7);
  cursor: pointer;
}

.fa-bars:active {
  transform: scale(0.95);
}

.menu {
  z-index: 9998;
  position: fixed;
  top: 0px;
  right: 0px;
  width: 20%;
  background-color: rgba(0, 0, 0, 0.9);
  height: 100vh;
}

@media screen and (max-height: 350px) {
  .menu {
    overflow-y: scroll;
    -webkit-overflow-scrolling: scroll;
  }
}

.menu .menu-items {
  display: block;
  color: rgb(255, 255, 255);
  text-align: center;
  padding: 15px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.8);
  transition: 0.4s ease-in-out;
}

.menu-items.first {
  border-top: 1px solid rgba(255, 255, 255, 0.8);
}

.menu .menu-items:hover {
  cursor: pointer;
  background-color: rgb(68, 67, 67);
}

.menu .menu-items:active {
  transform: scale(0.95);
}

.exit {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: rgb(255, 255, 255);
  padding: 15px 30px;
}

.close-menu {
  color: rgb(255, 255, 255);
}

.close-menu:hover {
  cursor: pointer;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

@media screen and (max-width: 700px) {
  .menu {
    width: 45%;
  }
  .exit h3 {
    font-size: 16px;
  }
}

@media screen and (min-width: 701px) and (max-width: 1000px) {
  .menu {
    width: 30%;
  }
}
</style>


