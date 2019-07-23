<template>
  <footer>
    <p>
      &copy; Vue Todo {{year}} by
      <span
        @click="delayUrlLoad('https://latishagriffiths.com/', 1000);return false;"
        class="personal-site-link"
      >Tish Griffiths</span>
    </p>
    <span
      @click="delayUrlLoad('https://github.com/TishG', 1000);return false;"
      class="fa fa-github"
    ></span>
  </footer>
</template>

<script>
export default {
  name: "Footer",
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

.fa-github,
.github-link {
  transition: all 1s ease-in-out;
  font-size: 24px;
}

.github-link:hover,
.fa-github:hover {
  color: rgba(0, 0, 0, 1);
  cursor: pointer;
}

.fa-github:active {
  transform: scale(0.5);
}

.github-link {
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
