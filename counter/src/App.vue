<template>
  <div id="app">
    <home></home>
  </div>
</template>

<script>

import home from "@/view/home.vue";

export default {
  name: 'App',
  components:{
    home
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  caret-color:transparent
}
</style>
