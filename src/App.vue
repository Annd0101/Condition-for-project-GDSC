<template>
  <div id="app">
   <Todos />
  </div>
</template>

<script>

import Todos from './components/Todos'
export default {
name: "App",
components: { Todos},

};
</script>


<style>
#app{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>