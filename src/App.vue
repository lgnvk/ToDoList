<template>
  <div class="app">
    <h1>Менеджер задач</h1>
    <Input v-model="searchQuery" placeholder="Поиск..."/>
    <div class="app_buttons">
      <Button @click="showModal">Новая задача</Button>
      <Selection v-model="selectedSort" :options="sortOptions"></Selection>
    </div>
    <ModalPage v-model:show="modalVisible">
      <TaskForm @create="createTask" />
    </ModalPage>
    <TaskList :tasks="searchedTasks" @remove="removeTask" @done="completedTask"/>
    <div class="page_wrapper">
      <div v-for="pageNumber in totalPages" :key="pageNumber" class="page"
      :class="{'current-page': page === pageNumber}" @click="changePage(pageNumber)">{{pageNumber}}</div>
    </div>
  </div>
</template>

<script>
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import axios from "axios";
export default {
  components: {
    TaskForm,
    TaskList,
  },
  data() {
    return {
      tasks: [],
      modalVisible: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По описанию'}
      ]
    };
  },
  methods: {
    createTask(task) {
      this.tasks.push(task);
      this.modalVisible = false;
    },
    removeTask(task) {
      this.tasks = this.tasks.filter((el) => el.id !== task.id);
    },
    completedTask(task) {
      task.completed = true;
      if (task.completed) {
        this.removeTask(task);
      }
    },
    showModal() {
      this.modalVisible = true;
    },
    async fetchTasks() {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10", {
            params: {
              _page: this.page,
              _limit: this.limit,
            }
          }
        );
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.tasks = response.data;
      } catch (err) {
        console.log("Data err");
      }
    },
    changePage(pageNumber) {
      this.page = pageNumber;
    },
  },
  mounted() {
    this.fetchTasks();
  },
  computed: {
    sortedTasks() {
      return [...this.tasks].sort((task1, task2) => task1[this.selectedSort]?.localeCompare(task2[this.selectedSort]))
    },
    searchedTasks() {
      return this.sortedTasks.filter(task => task.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    page() {
      this.fetchTasks();
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  padding: 20px;
}
.app_buttons {
  display: flex;
  justify-content: space-between;
}
.page_wrapper {
  display: flex;
}
.page {
  border: 1px solid black;
  padding: 10px;
}
.current-page {
  border: 2px solid red;
}
</style>