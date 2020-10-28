<template>
  <div id="app">
    <h1>Tarefas</h1>
    <TaskProgress :progresso="progresso" ></TaskProgress>
    <NewTask @taskAdded="addTask"/>
    <TasksGrid
        :tasks="tasks"
        @taskDeleted="deleteTask"
        @trocarEstado="toggleTaskState()"
    />
  </div>
</template>

<script>
import TasksGrid from "@/components/TasksGrid";
import NewTask from "@/components/NewTask";
import TaskProgress from "@/components/TaskProgress";
export default {
  components: {TasksGrid, NewTask, TaskProgress},
  data() {
    return {
      tasks: []
    }
  },
  computed:{
    progresso(){
      const total = this.tasks.length;
      const done = this.tasks.filter( t => !t.pending).length
      return Math.round(done/total *100) || 0
    }
  },
  methods: {
    addTask(task) {
      const sameName = t => t.name === task.name
      const reallyNew = this.tasks.filter(sameName).length == 0
      if(reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true
        })
      }
      console.log(task)
    },
    deleteTask(i) {
      this.tasks.splice(i, 1)
    },
    toggleTaskState(i) {
      this.tasks[i].pending = true

    }
  }
}

</script>

<style>
body {
  font-family: 'Lato', sans-serif;
  background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
  color: #FFF;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app h1 {
  margin-bottom: 5px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
