<template>
  <div class="task">
    <div>
      <div><strong>Название:</strong> {{ task.title }}</div>
      <div><strong>Описание:</strong> {{ task.body }}</div>
    </div>
    <div class="task_buttons">
      <Button @click="$emit('done', task)">Выполнено</Button>
      <Button @click="$emit('remove', task)">Удалить</Button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.task {
  margin-bottom: 15px;
  padding: 15px;
  border: 2px solid black;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.task_buttons {
  display: flex;
}
</style>