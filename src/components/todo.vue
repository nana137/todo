<template>
  <section class="real-app">
    <input type="text" class="add-input" autofocus placeholder="接下来要做什么？" @keyup.enter="addTodo">
    <Item :todo="todo" v-for="todo in filterTodos" :key="todo.id" @del="deleteTodo"></Item>
    <Tabs :filter="filter" :todos="todos" @toggle="toggleFilter" @clearAll="clearAllCompleted"></Tabs>
  </section>

</template>

<script>
  import Item from './item'
  import Tabs from './tabs'
  let id = 0;
  export default{
    data(){
      return {
        todos:[],
        filter:'全部'
      }
    },
    methods: {
      addTodo(e){
          this.todos.unshift({
              id:id++,
            content:e.target.value.trim(),
            completed:false
          });
        e.target.value = "";
      },
      deleteTodo(id){
          this.todos.splice(this.todos.findIndex(todo => todo.id === id),1);
      },
      toggleFilter(state){
          this.filter = state;
      },
      clearAllCompleted(){
          this.todos = this.todos.filter(todo => !todo.completed);
      }
    },
    computed:{
        filterTodos(){
            if(this.filter === '全部'){
                return this.todos;
            }
            const completed = this.filter === '已完成';
            return this.todos.filter(todo => completed === todo.completed);
        }
    },
    components: {
      Item,
      Tabs
    }
  }
</script>

<style>
  .real-app {
    width: 600px;
    margin: 0 auto;
    box-shadow: 0 0 5px #EE5C42;
  }

  .add-input {
    position: relative;
    width: 100%;
    font-size: 24px;
    line-height: 1.4rem;
    border: 0;
    outline: none;
    padding: 16px 16px 16px 60px;
    box-sizing: border-box;
  }
</style>
