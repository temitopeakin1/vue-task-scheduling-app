<template>
   <div v-show="showAddTask">
      <AddTask @add-task="addtask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'


export default {
  name: 'Home',
  props: {
    showAddTask: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
      return {
        tasks: [],
      }
    },

  methods: {
    //for data to persist across page refreshes
   async addtask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
         
        },
         body: JSON.stringify(task),
      })
      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
   async deleteTask(id) {
      if (confirm("Are you sure you want to delete task?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })

        res.status === 200 
        ? (this.tasks = this.tasks.filter(
          (task) => task.id !== id))
          : alert("Error deleting task");
      }
    },
    // updating the task to true or false, using MAP as a result of the Higher order array functions
     async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const update = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(update),
      })
     const data = await res.json();
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder 
        } : task
      )
      
    },
  

  async fetchTasks() {
    const res = await fetch("api/tasks");
    const data = await res.json();

    return data
  },
  // a lifesycle method in vue
 
  async fetchTask(id) {
    const res = await fetch(`api/tasks/${id}`);
    const data = await res.json();

    return data;
  },
},

 async created() {
    this.tasks = await this.fetchTasks();
  },
}

</script> 




