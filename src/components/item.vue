<template>
  <div :class="['todo-item',todo.completed ? 'completed' : '']">
    <input type="checkbox" class="toggle" v-model="todo.completed">
    <label>{{todo.content}}</label>
    <button class="destroy" @click="deleteTodo"></button>
  </div>
</template>
<script>
  export default{
      props:{
          todo:{
              type:Object,
            required:true
          }
      },
    methods:{
          deleteTodo(){
              this.$emit('del',this.todo.id);
          }
    }
  }
</script>
<style>
  .todo-item{
    position:relative;
    font-size:24px;
    border-bottom:1px solid #EE5C42;
  }
  .todo-item:hover .destroy:after{
    content:url('../assets/image/delete.svg')
  }
  .todo-item label{
    white-space:pre-line;
    word-break:break-all;
    padding:15px 60px 15px 15px;
    margin-left:45px;
    display:block;
    line-height:1.2;
    transition:color 0.4s;
  }
  .completed label{
    color: rgba(175,47,47,0.4);
    text-decoration:line-through;
  }
  .toggle{
    text-align:center;
    width:40px;
    height:40px;
    line-height:40px;
    position:absolute;
    top:8px;
    bottom:0;
    padding-left:5px;
    cursor:pointer;
    -webkit-appearance:none;    /*取消CheckBox的默认样式*/
    outline:none;  /*取消CheckBox选中状态的外边框*/
  }
  .toggle:after{
    content:url('../assets/image/round.svg');
  }
  .toggle:checked:after{
    content:url('../assets/image/done.svg');
  }
  .destroy{
    position:absolute;
    top:0;
    bottom:0;
    right:10px;
    width:40px;
    height:40px;
    margin:auto 0;
    font-size:30px;
    transition:color 0.2s ease-out;
    background-color:transparent;
    cursor:pointer;
    border:0;           /*将border为0，background-color为transparent可以取消button的默认样式*/
  }

</style>
