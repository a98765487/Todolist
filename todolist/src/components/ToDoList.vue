<template>
  <div>
    <div>
      <span>To Do List Demo：</span>
    </div>
    <div>
      <span
        ><input type="text" v-model="task" />
        <button @click="add(task)">新增</button>
      </span>
      <div>
        <li :key="todo.name" v-for="todo in todoList">
          <input type="checkbox" :checked="todo.completed" />{{ todo.name }}
          <button v-on:click="del(todo)">刪除</button>
        </li>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDoList",
  data() {
    return {
      todoList: [],
    };
  },
  props: {
    msg: String,
  },
  methods: {
    check(value) {
      this.todoList.forEach((todo) => {
        todo.completed = value;
      });
    },
    add(task) {
      this.todoList.push({ name: task, completed: false });
    },
    del(todo) {
      this.todoList.splice(this.todoList.indexOf(todo), 1);
    },
  },
};
</script>

<style scoped>
</style>
