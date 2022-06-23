<template>
  <div v-if="tasks.length > 0">
    <h3>Список поcтов</h3>
    <TaskItem v-for="task in tasks" :task="task" :key="task.id" @remove="$emit('remove', task)" @done="$emit('done', task)"/>
  </div>
  <h2 v-else>
    Список задач пуст
  </h2>
</template>

<script>
import TaskItem from './TaskItem.vue';
export default {
  components: {
    TaskItem,
  },
  props: {
    tasks: {
      type: Array,
      required: true,
    }
  }
};
</script>

<style scoped>
h3 {
  margin-bottom: 15px;
}
</style>