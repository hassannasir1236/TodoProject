<template>
    <div class="input-container">
        <input type="text" v-model="addtask" placeholder="Enter your task">
        <button @click="Addtask">Add Task</button>
    </div>
    <div class="Container">
        <div class="row">
            <AllStatic :tasks="task" @updateStatus="updateTaskStatus"/>
            <TodoTask :tasks="task" @updateStatus="updateTaskStatus" @updatedTaskName="updateTaskName"/>
            <CompletedTask  :tasks="task" @updateStatus="updateTaskStatus" />
            <PendingTask :tasks="task" @updateStatus="updateTaskStatus" @updatedTaskName="updateTaskName"/>
            <DeletedTask :tasks="task" @updateStatus="updateTaskStatus" @deleteTaskById="deleteTaskById"/>
        </div>
        <p>Created by Muhammad Hassan Nasir</p>
    </div>
</template>

<script>
import AllStatic from './AllStatic.vue';
import CompletedTask from './CompletedTask.vue';
import PendingTask from './PendingTask.vue';
import DeletedTask from './DeletedTask.vue';
import TodoTask from './TodoTask.vue';
export  default {
  name: 'AddTask',
  data(){
    return {
      addtask: '',
      task: [],
    }
  },
  components: {
    AllStatic,
    PendingTask,
    CompletedTask,
    DeletedTask,
    TodoTask,
  },
  mounted() {
        const tasks = localStorage.getItem("tasks");
        if (tasks) {
          this.task = JSON.parse(tasks);
        }
  },
  methods: {
    Addtask(){
        if (this.addtask.trim()) {
        const newTask = {
          id: Date.now(),  
          name: this.addtask,  
          is_completed: false,
          is_pending: false,
          is_deleted: false,
          is_todo: true,
        };
        this.task.push(newTask);
        localStorage.setItem("tasks", JSON.stringify(this.task));
        this.addtask = '';
      }
    },
    updateTaskStatus(taskId, statusKey, value) {
        const storedTasks = localStorage.getItem("tasks");
        if (storedTasks) {
            const tasks = JSON.parse(storedTasks);
            const task = tasks.find(t => t.id === taskId);
            if (task) {
                task[statusKey] = value;
                if (value === true) {
                    const statusKeys = ['is_completed', 'is_pending', 'is_deleted', 'is_todo'];
                    statusKeys.forEach(key => {
                        if (key !== statusKey) {
                            task[key] = false;
                        }
                    });
                }
                localStorage.setItem("tasks", JSON.stringify(tasks));
                this.task = [...tasks];
            }
        }
    },
    deleteTaskById(taskId) {
        const storedTasks = localStorage.getItem("tasks");

        if (storedTasks) {
            const tasks = JSON.parse(storedTasks);
            const updatedTasks = tasks.filter(task => task.id !== taskId);
            localStorage.setItem("tasks", JSON.stringify(updatedTasks));
            this.task = updatedTasks;
        }
    },
    updateTaskName(taskId, taskname){
        const storedTasks = localStorage.getItem("tasks");
        if (storedTasks) {
            const tasks = JSON.parse(storedTasks);
            const task = tasks.find(t => t.id === taskId);
            if (task) {
                task['name'] = taskname;
                localStorage.setItem("tasks", JSON.stringify(tasks));
                this.task = [...tasks];
            }
        }
    }
  }
}
</script>
<style scoped>
.Container {
    width: 33.3%;
    text-align: center;
    margin-bottom: 15px;
    margin-top: 30px;
}   
.Container > * {
    margin-right: 20px; 
}
.input_container{
    margin-top: 75px;
    height: auto;
    width: 100%;
}
.row {
    margin: 20px 0;
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    width: 90vw;
}
.Center_Container {
    width: 100%;
    text-align: center;
}
.Center_Container > * {
    margin-right: 20px; 
}
.input-container {
      position: relative;
      width: 500px;
      margin: 55px auto;
    }

.input-container input {
    width: 100%;
    padding: 10px 50px 10px 15px; 
    font-size: 16px;
    border: 2px solid #ccc;
    border-radius: 25px;
    outline: none;
    box-sizing: border-box;
}

.input-container input:focus {
    border-color: #3cd9a0;
}

.input-container button {
    position: absolute;
    top: 50%;
    right: 10px;
    transform: translateY(-50%);
    background-color: #6B81EF;
    color: white;
    border: none;
    padding: 8px 15px;
    border-radius: 20px;
    font-size: 14px;
    cursor: pointer;
    outline: none;
}

.input-container button:hover {
    background-color: #2bbf89;
}
/* .Container > *:last-child {
    margin-right: 0; 
} */
</style>