<template>
  <main class="bg-neutral-900">
    <section class="todo">
      <div class="container max-w-3xl mx-auto px-4 bg-neutral-800">
        <div class="todo__create flex w-96 relative mx-auto py-6">
          <input
            v-model="task"
            @keydown.enter="addTask"
            type="text"
            class="create__title w-full p-2 font-semibold"
            placeholder="Your task" />
          <div
            @click="addTask"
            class="create-btn active:scale-110 duration-150 bg-emerald-500 w-fit cursor-pointer">
            <i class="create-plus p-2 fa-solid fa-plus"> </i>
          </div>
        </div>
        <hr />
        <div class="todo__list">
          <div
            v-for="task in tasks"
            class="todo__item flex justify-between mt-4 items-center mx-auto bg-white">
            <p
              :class="{
                'line-through': task.complete,
              }"
              class="todo__text font-semibold p-2">
              {{ task.text }}
            </p>
            <div class="todo__actions flex items-center mr-3">
              <i
                @click="deleteTask(task.id)"
                class="cursor-pointer mr-3 hover:text-red-700 active:scale-110 duration-300 text-xl fa-solid fa-trash-can"></i>
              <div
                @click="completeTask(task.id)"
                :class="{
                  'hover:bg-red-600 hover:border-red-600': task.complete,
                  'hover:bg-green-500 hover:border-green-500': !task.complete,
                }"
                class="todo__check cursor-pointer border-2 active:scale-110 border-black duration-200">
                <i v-if="!task.complete" class="p-1 fa-solid fa-check"></i>
                <i v-else class="py-1 fa-solid fa-xmark"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      task: '',
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.task !== '') {
        const task = { id: Date.now(), text: this.task, complete: false };
        this.tasks = [task, ...this.tasks];
        this.task = '';
      }
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((obj) => obj.id !== id);
    },
    completeTask(id) {
      const findedTask = this.tasks.find((obj) => obj.id === id);
      findedTask.complete = !findedTask.complete;
    },
  },
};
</script>

<style lang="sass" scoped>
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
