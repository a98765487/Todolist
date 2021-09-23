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
              rounded-none
              sm:text-sm
              border-gray-300
              enter-input
            "
            placeholder="enter to add todo"
          />
        </span>
        <div class="flex items-start" :key="todo.id" v-for="todo in todoList">
          <transition name="fade">
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
                <i class="fas fa-trash"></i>
              </button>
            </div>
          </transition>
        </div>
      </div>
    </div>
    <div class="shadow overflow-hidden sm:rounded-md">
      <div class="px-4 py-5 sm:px-6">
        <h3 class="text-lg leading-6 font-medium text-gray-900">Completed：</h3>
        <span
          class="text-md transition-opacity"
          :key="todo.id"
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
  methods: {
    check(value) {
      this.todoList.forEach((todo) => {
        todo.completed = value;
      });
    },
    randomKey() {
      return Math.floor(Math.random() * 1000000) + 1;
    },
    add(task) {
      if (!task) return;

      this.todoList.push({
        id: this.randomKey(),
        name: task,
        completed: false,
      });
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
  transition: opacity ease 0.25s, transform ease-in-out 0.3s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateX(100%);
}

.enter-input:focus {
  border-bottom: 1px solid #ddd;
}
</style>
