<template>
   <div class="Container">
        <div class="row">
            <h1>Completed Task</h1>
        </div>
        <!-- Cards Container -->
        <div class="cards-container">
            <div class="card"  v-for="task in filteredTasks" :key="task.id">
                <div>
                    <span class="card-title">{{ task.name }}</span>
                </div>
                <div class="card-button-div">
                    <button class="card-btn" @click="markAsTodo(task.id)">R</button>
                    <button class="card-btn" @click="markAsPending(task.id)">P</button>
                    <button class="card-btn" @click="markAsDeleted(task.id)">D</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>    
export default {
    name: 'CompletedTask',
    props: {
        tasks: Array,  
    },
    components: {
    },
    computed: {
        filteredTasks() {
            return this.tasks.filter(tasks => tasks.is_completed === true);
        },
    },
    methods: {
        markAsCompleted(taskId) {
            this.$emit('updateStatus', taskId, 'is_completed', true); 
        },
        markAsPending(taskId) {
            this.$emit('updateStatus', taskId, 'is_pending', true); 
        },
        markAsDeleted(taskId) {
            this.$emit('updateStatus', taskId, 'is_deleted', true); 
        },
        markAsTodo(taskId) {
            this.$emit('updateStatus', taskId, 'is_todo', true); 
        },
    }
}
</script>
<style scoped>
.Container {
    margin: 0 auto;
    width: 33.3%;
    text-align: center;
    border: 5px solid #4EEE49;
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
    background-color: rgb(60, 217, 68);
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
    background-color: #5ff2a4;
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
  .card-button-div{
    padding: 2px 0px;
    width: 60px;
  }
  .card-btn{
    font-weight: 700;
    height: 18px;
    width: 18px;
    border-width: initial;
    border-style: none;
    border-color: initial;
    border-image: initial;
    border-radius: 4px;
    margin: 5px;
    text-align: center;
  }
</style>