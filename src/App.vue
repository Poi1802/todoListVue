<template>
  <main class="bg-neutral-900">
    <section class="todo">
      <div class="container max-w-3xl mx-auto px-4 bg-neutral-800">
        <CreateTodo @clickAdd="addTask" @pressEnter="addTask" />
        <hr />
        <TodoList :tasks="tasks" @clickTrash="deleteTask" @clickCheck="completeTask" />
      </div>
    </section>
  </main>
</template>

<script>
import CreateTodo from './components/CreateTodo.vue';
import TodoList from './components/TodoList.vue';

export default {
  data() {
    return {
      tasks: [],
    };
  },
  components: {
    CreateTodo,
    TodoList,
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem('todos'));
  },
  methods: {
    addTask(task) {
      if (task === '') {
        return;
      }

      const todo = { id: Date.now(), text: task, complete: false };
      this.tasks = [todo, ...this.tasks];
      localStorage.setItem('todos', JSON.stringify(this.tasks));
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((obj) => obj.id !== id);
      localStorage.setItem('todos', JSON.stringify(this.tasks));
    },
    completeTask(id) {
      const findedTask = this.tasks.find((obj) => obj.id === id);
      console.log(id);
      findedTask.complete = !findedTask.complete;
      localStorage.setItem('todos', JSON.stringify(this.tasks));
    },
  },
};
</script>

<style lang="sass">
main
  min-height: 100vh
  .container
    border-radius: 20px
    min-height: 100vh
    .create__title
      border-radius: 10px
    .create-btn
      border-radius: 50%
      position: absolute
      right: -10px
      top: 22px
      transition: 0.2s ease-in-out
      .create-plus
        font-size: 28px
        transition: 0.15s ease-in-out
        &:hover
          transform: scale(1.1)
    .todo__item
      width: 70%
      border-radius: 8px
    .todo__check
      border-radius: 50%
      .fa-xmark
        padding-inline: 7px
</style>
