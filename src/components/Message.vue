<template>
  <div class="message-comp">
    <transition name="fade" class="container">
      <div class="message" v-show="displayMessage.show">
        <p>{{ displayMessage.m1 }}</p>
        <p>{{ displayMessage.m2 }}</p>
        <!-- <button class="yes" @click="$emit('clear-todos')">Yes</button> -->
        <button
          v-if="
            displayMessage.m1 == 'Are you sure you want to delete this list?'
          "
          v-show="
            displayMessage.m1 !== 'Action Omitted: List is already empty.'
          "
          class="yes"
          @click="$emit('clear-todos')"
        >
          Yes
        </button>
        <button
          v-show="
            displayMessage.m1 !== 'Action Omitted: List is already empty.'
          "
          v-else
          class="yes"
          @click="$emit('del-todo')"
        >
          yes
        </button>
        <button
          v-show="
            displayMessage.m1 !== 'Action Omitted: List is already empty.'
          "
          class="no"
          @click="$emit('close-message')"
        >
          No
        </button>
        <button
          v-show="
            displayMessage.m1 === 'Action Omitted: List is already empty.'
          "
          @click="$emit('close-message')"
        >
          close
        </button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: ["displayMessage"]
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.message-comp {
  width: 100%;
  display: flex;
  justify-content: center;
}

.message p {
  color: rgb(255, 0, 0);
  font-weight: bold;
}

.message {
  position: absolute;
  top: 30%;
  z-index: 9999;
  background-color: rgb(255, 255, 255);
  width: 40%;
  margin: 0 auto;
  padding: 10px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  line-height: 1.5rem;
  text-align: center;
}

.message button {
  margin-top: 10px !important;
  padding: 5px 10px !important;
  border-radius: 3px !important;
  background-color: transparent !important;
  border: 1.5px solid rgb(0, 0, 0) !important;
  color: rgb(0, 0, 0) !important;
  transition: 0.5s all ease-in-out;
  cursor: pointer;
}

.message > button:active {
  transform: scale(0.9);
}

.message > button:focus {
  outline: none;
}

.yes {
  margin-right: 3px;
}

.no {
  margin-left: 3px;
}

@media screen and (max-width: 900px) {
  .message {
    width: 80%;
  }
}
</style>
