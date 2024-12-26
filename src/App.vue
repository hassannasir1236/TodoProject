<template>
  <div class="Container">
    <div class="main">
      <h1 class="main-heading">ToDo List</h1>
    </div>
      <div>
        <AddTask />
      </div>  
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue';
export default {
  name: 'App',
  components: {
    AddTask,
  }
}
</script>

<style>
body{
  background-color: #6B81EF;
  width: 100%;
  overflow-x: hidden;
}
.Container{

}
.main{
  width: 100%;
  height: 30px;
  text-align: center;
  display: flex;
  justify-content: center;
}
.main-heading{
  color: white;
  transition: transform 10s cubic-bezier(0, 0.27, 0, 1.44);
  width: 300px;
  height: 30px;
  text-align: center;
  margin-bottom: 30px;
}
.main-heading:hover {
  transform: scale(1.5); 
  width: 100%;
  height: 30px;
  overflow-x: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
