<template>
  <div id="app">
    <div id="cover">
      <Header></Header>
      <Todo></Todo>
    </div>
  </div>
</template>

<script>
  import Header from "@/components/Header.vue";
  import Todo from "@/components/Todo.vue";
  export default {
    name: "App",
    components: {
      Header,
      Todo,
    },
  };
</script>

<style>
  #cover {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: #999;
    opacity: 0.9;
    z-index: -1;
  }
</style>
