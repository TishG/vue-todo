<template>
  <h1>{{title}}</h1>
</template>

<script>
export default {
  name: "Header",
  props: ["title"]
};
</script>

<style scoped>
h1 {
  padding: 20px 30px;
  height: 70px;
}
</style>


