<template>
  <form @submit.prevent>
    <h3>Создание поста</h3>
    <Input
      v-model="task.title"
      placeholder="Название"
    />
    <Input
      v-model="task.body"
      placeholder="Описание"
    />
    <Button @click="createTask">Добавить</Button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: "",
        body: "",
        completed: false,
      },
    };
  },
  methods: {
    createTask() {
      this.task.id = Date.now();
      this.$emit('create', this.task);
      this.task = {
        title: "",
        body: "",
      }
      
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
Button {
  align-self: flex-end;
}
h3 {
  margin-bottom: 15px;
}
</style>