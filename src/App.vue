<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">SIMPLE TODO APP</h5>
        <div class="row">
          <div class="col-10">
            <input
              v-model="todo"
              type="text"
              class="form-control"
              @keyup.enter="add" />
          </div>
          <div class="col-2">
            <button class="btn btn-success text-white shadow" @click="add">
              ADD +
            </button>
          </div>
        </div>
        <Search @searchItem="searchItem" />
        <List :todos="AllData" @deleteTodo="deleteTodo" @doneTodo="doneTodo" />
        <br />
        <small class="fw-bold">Total TODO : {{ totalTODO }} </small>
        <br />
        <small class="text-success fw-bold"
          >TODO done: {{ totalTodoDone }}</small
        >
        <br />
        <small class="text-danger fw-bold"
          >TODO not Done:
          {{ parseInt(totalTODO) - parseInt(totalTodoDone) }}</small
        >
      </div>
    </div>
  </div>
</template>

<script>
import List from "./components/List.vue";
import Search from "./components/Search.vue";
export default {
  components: { List, Search },
  data() {
    return {
      todo: "",
      todos: [],
      searchValue: "",
    };
  },
  mounted() {
    this.todos = localStorage.getItem("todos")
      ? JSON.parse(localStorage.getItem("todos"))
      : [];
  },
  computed: {
    totalTODO() {
      return this.todos.length;
    },
    AllData() {
      return this.todos.filter(
        (item) =>
          item.activity.toLowerCase().includes(this.searchValue) ||
          item.activity.toUpperCase().includes(this.searchValue)
      );
    },
    totalTodoDone() {
      return this.todos.filter((item) => item.isDone).length;
    },
  },
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false,
      });
      this.saveToLocalStorage();
      this.todo = "";
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index !== todoIndex) {
          return item;
        }
      });
      this.saveToLocalStorage();
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index === todoIndex) {
          item.isDone = !item.isDone;
        }

        return item;
      });
      this.saveToLocalStorage();
    },
    searchItem(searchItem) {
      this.searchValue = searchItem;
    },
    saveToLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style></style>
