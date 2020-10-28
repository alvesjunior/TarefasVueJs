<template>
  <div class="tasks-grid">
    <template v-if="tasks.length > 0">
      <Taskk v-for="(task, i) in tasks" :Key="task.name"
             @taskDeleted="$emit('taskDeleted', i) "
             @trocarEstado="$emit('trocarEstado', i)"
             :task="task">
      </Taskk>
      {{tasks}}
    </template>
    <p class="no-task" v-else>
      <span>Sua vida está em dia</span>
    </p>
  </div>
</template>
<script>
import Taskk from "@/components/Taskk";

export default {
  components: {Taskk},
  props: {
    tasks: {type: Array, required: true}
  }
}


</script>
<style scoped>
.tasks-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.task-grid .task {
  margin: 10px;
}

.no-task {
  color: #aaa;
  font-size: 1.7rem;
}
</style>