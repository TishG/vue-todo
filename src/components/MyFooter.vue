<template>
  <footer>
    <p>{{ title }} &copy;&nbsp;{{ year }}</p>
    <span
      @click="
        delayUrlLoad('https://latishagriffiths.com/', 1000);
        return false;
      "
    >
      <i class="fas fa-link"></i>
    </span>
  </footer>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["title"],
  computed: {
    year() {
      return new Date().getFullYear();
    }
  },
  methods: {
    delayUrlLoad(url, mils) {
      setTimeout(function() {
        window.open(url);
      }, mils);
    }
  }
};
</script>

<style>
@media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
  /* IE10+ CSS styles go here */
  footer {
    position: fixed;
    bottom: 0;
  }
}
footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 40px;
  width: 100%;
  margin-top: auto;
  padding: 0px 30px;
  background-color: rgba(5, 103, 149, 0.4);
  color: rgba(255, 255, 255, 1);
  box-shadow: 0px 0px 10px 10px rgba(5, 103, 149, 0.4);
  font-size: 14px;
}

ion-icon {
  transition: all 1s ease-in-out;
  font-size: 20px;
}

ion-icon:hover {
  color: rgba(0, 0, 0, 1);
  cursor: pointer;
}

ion-icon:active {
  transform: scale(0.5);
}

ion-icon {
  color: rgba(255, 255, 255, 1);
}

.personal-site-link {
  color: rgba(255, 255, 255, 1);
  text-decoration: none;
  transition: all 1s ease-in-out;
}

.personal-site-link:hover {
  color: rgba(0, 0, 0, 1);
  font-weight: bold;
  cursor: pointer;
}

.personal-site-link:active {
  transform: scale(0.5);
}
</style>
