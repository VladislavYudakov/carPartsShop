<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <div class="p-4">
      <b-icon icon="table" _animation="throb" font-scale="7.5" shift-v="8"></b-icon>
      <h3 > Scheduler </h3>
    </div>

<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <MultipleFile />
<!--    <MyTable />-->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import MyTable from './components/MyTable.vue'
import MultipleFile from './components/MultipleFile.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    // MyTable,
    MultipleFile
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
