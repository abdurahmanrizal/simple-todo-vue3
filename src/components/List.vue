<template>
  <div class="mt-4">
    <ul class="list-group">
      <li class="list-group-item" v-for="(todo, index) in todos" :key="index">
        <div class="row">
          <div class="col">
            <span
              :class="[
                { 'text-danger': todo.isDone },
                { 'line-through': todo.isDone },
              ]"
              >{{ todo.activity }}</span
            >
          </div>
          <div class="col-auto">
            <div class="row gx-2">
              <div class="col">
                <button
                  class="btn btn-primary text-white shadow"
                  @click="doneTODO(index)"
                  v-if="!todo.isDone">
                  DONE
                </button>
                <button
                  class="btn btn-warning text-white shadow"
                  @click="doneTODO(index)"
                  v-else>
                  UNDONE
                </button>
              </div>
              <div class="col">
                <button
                  class="btn btn-danger shadow"
                  @click="deleteTODO(index)">
                  x
                </button>
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    },
  },

  methods: {
    deleteTODO(index) {
      this.$emit("deleteTodo", index);
    },
    doneTODO(index) {
      this.$emit("doneTodo", index);
    },
  },
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
