<template>
  <div class="container">

    <Header_Comp
        @toggle-add-task="toggleAddTask"
        :showAddTask = 'showAddTask'
    />

    <div v-show="showAddTask">
      <add_Task @add-task="addTask"/>
    </div>

    <Tasks_Comp
        @toggle-reminder="toggleReminder"
        @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header_Comp from "./components/Header_Comp"
import Tasks_Comp from "./components/Tasks"
import add_Task from "./components/addTask"
export default {
  name: 'App',
  components:{
    // eslint-disable-next-line vue/no-unused-components
    Header_Comp,
    Tasks_Comp,
    add_Task,
  },
  data(){
    return {
      tasks: [],
      showAddTask:false,
    }
  },
 async created() {
    this.tasks = await this.fetchTasks()
  },
  methods:{
  async  deleteTask(id){
      if(confirm('Are you sure ?')){
        const resquest = await fetch(`api/tasks/${id}`,
            {
              method:'DELETE',
            })
               resquest.status === 200
              ? (this.tasks = this.tasks.filter((task) => task.id !== id))
              : alert('Error deleting task')
      }
    },

  async  toggleReminder(id){
     const taskToggle = await this.fetchSingleTask(id)
     const update = {...taskToggle,reminder:!taskToggle.reminder}

     const request = await fetch(`api/tasks/${id}`,
         {
           method:'PUT',
           headers: {
             'Content-type':'application/json'
           },
           body:JSON.stringify(update)
         })
         const data = await request.json()
      this.tasks = this.tasks.map((task)=> task.id === id
      ? {...task, reminder: data.reminder} : task )
    },

    async fetchTasks(){
      const result = await fetch('api/tasks')
      const data = await  result.json()

      return data
    },

    async fetchSingleTask(id){
      const result = await fetch(`api/tasks/${id}`)
      const data = await  result.json()

      return data
    },

   async addTask(task){
      const result = await fetch('api/tasks', {
        method: 'POST',
        headers:{
          'content-type':'application/json',
        },
        body:JSON.stringify(task)

      })
      const data = await result.json()
      this.tasks = [...this.tasks, data]
    },

    toggleAddTask(){
      this.showAddTask = !this.showAddTask
       },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;

}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
