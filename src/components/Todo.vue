<template>
  <div class="main">
    <input
      type="text"
      class="addInput"
      autofocus="autofocus"
      placeholder="接下来要做什么？"
      @keyup.enter="addTodo"
    />
    <Item
      :todo="todo"
      v-for="todo in filteredTodos"
      :key="todo.id"
      @del="deleteTodo"
    ></Item>
    <Tabs
      :filter="filter"
      :todos="todos"
      @toggle="toggleFilter"
      @clearAllCompleted="clearAllCompleted"
    ></Tabs>
  </div>
</template>

<script>
  import Item from "@/components/Item.vue";
  import Tabs from "@/components/Tabs.vue";
  let id = 0;
  export default {
    name: "Todo",
    data() {
      return {
        todos: [],
        filter: "all",
      };
    },
    computed: {
      filteredTodos() {
        if (this.filter === "all") {
          return this.todos;
        }
        const completed = this.filter === "completed";
        return this.todos.filter((todo) => todo.completed === completed);
      },
    },
    methods: {
      addTodo(e) {
        if (e.target.value) {
          this.todos.unshift({
            id: id++,
            content: e.target.value.trim(),
            completed: false,
          });
          e.target.value = "";
        } else {
          alert("请先输入你想做的事情！");
        }
      },
      deleteTodo(id) {
        this.todos.splice(
          this.todos.findIndex((todo) => todo.id === id),
          1
        );
      },
      toggleFilter(state) {
        this.filter = state;
      },
      clearAllCompleted() {
        this.todos = this.todos.filter((todo) => !todo.completed);
      },
    },
    components: {
      Item,
      Tabs,
    },
  };
</script>

<style scoped>
  .main {
    width: 600px;
    margin: 0 auto;
    box-shadow: 0 0 5px #666;
  }
  .addInput {
    position: relative;
    margin: 0;
    width: 100%;
    font-size: 24px;
    font-family: inherit;
    font-weight: inherit;
    line-height: 1.4em;
    border: 0;
    outline: none;
    color: inherit;
    padding: 6px;
    border: 1px solid #999999;
    box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0);
    box-sizing: border-box;
    font-smoothing: antialiased;
    padding: 16px 16px 16px 60px;
    border: none;
    box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0);
  }
</style>
