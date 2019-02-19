<template>
  <div id="app">
    <task-header></task-header>
    <task-input v-on:addTask="addTask"></task-input>
    <task-list v-bind:propsdata="items" v-on:removeTask="removeTask"></task-list>
    <task-footer v-on:clearTask="clearTask"></task-footer>
  </div>
</template>

<script>
  import TaskHeader from "./components/taskHeader";
  import TaskInput from "./components/taskInput";
  import TaskList from "./components/taskList";
  import TaskFooter from "./components/taskFooter";

  export default {
    data() {
      return {
        items: []
      }
    },
    methods: {
      addTask(item) {
        localStorage.setItem(item, item);
        this.items.push(item);
      },
      removeTask(item, index) {
        localStorage.removeItem(item);
        this.items.splice(index, 1);
      },
      clearTask() {
        localStorage.clear();
        this.items=[];
      }
    },
    created() {
      if(localStorage.length>0) {
        for(let i=0; i<localStorage.length; i++) {
          this.items.push(localStorage.key(i));
        }
      }
    },
    components: {
      'task-header': TaskHeader,
      'task-input': TaskInput,
      'task-list': TaskList,
      'task-footer': TaskFooter
    }
  }
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>
