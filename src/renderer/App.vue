<template>
  <div id="app">
    <Header></Header>
    <router-view></router-view>
  </div>
</template>


<script>
import Header from "@/components/header.vue";
export default {
  components: { 
    Header 
  },
}
  
</script>

<style>
*{
    background-repeat: no-repeat;
    padding: 0;
    margin: 0;
}
</style>
