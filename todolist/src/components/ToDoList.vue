<template>
  <div class="bg-white shadow overflow-hidden sm:rounded-lg">
    <div class="px-4 py-5 sm:px-6">
      <h3 class="text-lg leading-6 font-medium text-gray-900">
        To Do List Demo：
      </h3>
    </div>
    <div class="shadow overflow-hidden sm:rounded-md">
      <div class="px-4 py-5 bg-white space-y-6 sm:p-6">
        <span
          ><input
            type="text"
            v-model="task"
            @keydown.enter="add(task)"
            class="
              focus:outline-none
              flex-1
              block
              rounded-none rounded-r-md
              sm:text-sm
              border-gray-300
            "
            placeholder="enter to add todo"
          />
        </span>
        <div class="flex items-start" :key="todo.name" v-for="todo in todoList">
          <div class="flex items-center h-5">
            <label class="font-medium text-gray-700 mr-1">
              <input
                name="todo"
                type="checkbox"
                v-model="todo.completed"
                class="
                  checked:bg-blue-600
                  checked:border-transparent
                  focus:ring-indigo-500
                  h-4
                  w-4
                  text-indigo-600
                  border-gray-300
                  rounded
                "
              />
              {{ todo.name }}</label
            >
            <button
              v-on:click="del(todo)"
              class="
                text-white text-sm
                inline-block
                py-1
                px-2
                bg-red-500
                text-white
                font-semibold
                rounded-lg
                shadow-md
                hover:bg-red-700
                focus:outline-none
              "
            >
              del
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="shadow overflow-hidden sm:rounded-md">
      <div class="px-4 py-5 sm:px-6">
        <h3 class="text-lg leading-6 font-medium text-gray-900">Completed：</h3>
        <span
          class="text-md transition-opacity"
          :key="todo.name"
          v-for="todo in todoList"
        >
          <transition name="fade">
            <li class="list-disc" v-if="todo.completed">
              {{ todo.name }}
            </li>
          </transition>
        </span>
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
      if (!task) return;

      this.todoList.push({ name: task, completed: false });
      this.task = "";
    },
    del(todo) {
      this.todoList.splice(this.todoList.indexOf(todo), 1);
    },
  },
};
</script>


<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
