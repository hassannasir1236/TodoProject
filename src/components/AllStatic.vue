<template>
    <div class="Container">
      <!-- Heading -->
      <div class="row">
        <h1>All Static</h1>
      </div>
      
      <!-- Cards Container -->
      <div class="cards-container">
        <div class="card">
          <span class="card-title">Total Tasks</span>
          <p class="card-title">{{ totoalCount }}</p>
        </div>
        <div class="card">
          <span class="card-title">Todo Tasks</span>
          <p class="card-title">{{ todoCount }}</p>
        </div>
        <div class="card">
          <span class="card-title">Completed Tasks</span>
          <p class="card-title">{{ completedCount }}</p>
        </div>
        <div class="card">
          <span class="card-title">Pending Tasks</span>
          <p class="card-title">{{ pendingCount }}</p>
        </div>
        <div class="card">
          <span class="card-title">Deleted Tasks</span>
          <p class="card-title">{{ deletedCount }}</p>
        </div>
        <!-- Add more cards if needed -->
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "AllStatic",
    props: {
        tasks: Array,  
    },
    computed: {
        totoalCount() {
            return this.tasks.length;
        },
        completedCount() {
            return this.tasks.filter(tasks => tasks.is_completed).length;
        },
        deletedCount() {
            return this.tasks.filter(tasks => tasks.is_deleted).length;
        },
        pendingCount() {
            return this.tasks.filter(tasks => tasks.is_pending).length;
        },
        todoCount() {
            return this.tasks.filter(tasks => tasks.is_todo).length;
        },
    },
  };
  </script>
  
  <style scoped>
  .Container {
    margin: 0 auto;
    width: 33.3%;
    text-align: center;
    border: 5px solid #3cd9a0;
    border-radius: 30px;
    height: 500px;
    overflow: hidden; 
    display: flex;
    flex-direction: column;
  }
  
  .row {
    margin: 20px 0;
    width: 100%;
    text-align: center;
    display: flex;
    justify-content: center;
  }
  
  h1 {
    background-color: rgb(60, 217, 160);
    box-shadow: rgb(0, 0, 0) 10px 10px 10px;
    color: rgb(255, 255, 255);
    font-size: 2.1rem;
    text-align: center;
    width: 88%;
    border-radius: 10px;
    margin: 15px 0;
    padding: 3px;
  }
  
  .cards-container {
    flex: 1; 
    overflow-y: auto;
    padding: 0px 0px 8px 18px;

  }
  
.card {
    background-color: #85ecc6;
    border-radius: 10px;
    padding: 0px 20px;
    box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 10px 15px;
    transition: transform 0.3s cubic-bezier(0.18, 0.32, 0.68, 0.89), box-shadow 0.3s ease;; 
}
.card:hover {
    transform: translateY(-5px); 
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    background-color: #74d3b5;
}
.card-title {
    font-weight: 800;
    color: #000000;
}
  </style>
  