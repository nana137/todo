<template>
  <div class="helper">
    <span class="left">{{unfinishedTodoLength}}项未完成</span>
    <span class="tabs">
      <span v-for="state in states" :key="state" :class="[state,filter == state ? 'actived' : '']"
            @click="toggleFilter(state)">{{state}}</span>
    </span>
    <span class="clear" @click="clearAllCompleted">清除已完成</span>
  </div>
</template>

<script>
  export default{
    props: {
      filter: {
        type: String,
        required: true,
      },
      todos:{
          type:Array,
        required:true,
      }
    },
    data(){
      return {
        states: ['全部', '进行中', '已完成']
      }
    },
    methods: {
      clearAllCompleted(){
          this.$emit('clearAll')
      },
      toggleFilter(state){
          this.$emit('toggle',state);
      }
    },
    computed:{
        unfinishedTodoLength(){
            return this.todos.filter(todo => !todo.completed).length;
        }
    }
  }
</script>

<style>
  .helper{
    font-weight:100;
    display:flex;
    justify-content:space-between;
    padding:5px 0;
    line-height:30px;
    font-size:14px;
  }
  .left, .tabs, .clear{
    padding:0 10px;
    box-sizing:border-box;
  }
  .left, .clear{
    width:150px;
  }
  .left{
    text-align:left;
  }
  .clear{
    text-align:right;
    cursor:pointer;
  }
  .tabs{
    width:260px;
    display:flex;
    justify-content:space-around;
  }
  .tabs span{
    display:inline-block;
    padding:0 10px;
    cursor:pointer;
  }
  .tabs .actived{
    color: crimson;
    font-weight:bold;
    font-size:16px;
  }
</style>
