<template>
  <div id="footer">
    <span>{{author}}   记</span>
  </div>
</template>

<script>
  export default{
      data(){
          return {
              author:'lina'
          }
      }
  }
</script>
<style scoped>
  #footer{
    margin-top:40px;
    text-align:center;
    color: rgba(175,47,47,0.4);
    font-size:18px;
    text-shadow:0 1px 0 1px;
    font-weight:bold;
  }
</style>
