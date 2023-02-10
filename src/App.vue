<template>
  <div id="app">
    <div  class="container my-5 w-75 p-3">
      <search/>
    </div>
  </div>
</template>

<script>

import search from "./components/Search"

export default {
  components:{
    search
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    outline: none;
  }
  body{
    background-color:#d8d7d8 ;
  }
  .container{
    background-color: #ebeef1 !important;
  }
  .custom-span{
    font-size: 14px;
  }
</style>
