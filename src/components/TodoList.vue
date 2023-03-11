<template>
  <div class="todo__list">
    <TransitionGroup name="bounce">
      <div
        v-for="task in tasks"
        :key="task.id"
        class="todo__item flex justify-between mt-4 items-center mx-auto bg-white">
        <div>
          <p
            :class="{
              'line-through': task.complete,
            }"
            class="todo__text font-semibold p-2">
            {{ task.text }}
          </p>
          <div
            v-if="task.deadline"
            :class="{
              'line-through': task.complete,
            }"
            class="deadline pl-2 pb-1 font-semibold italic">
            Deadline: {{ task.deadline }}
          </div>
        </div>
        <div class="todo__actions flex items-center mr-3">
          <i
            @click="$emit('clickTrash', task.id)"
            class="cursor-pointer mr-3 hover:text-red-700 active:scale-110 duration-300 text-xl fa-solid fa-trash-can"></i>
          <div
            @click="$emit('clickCheck', task.id)"
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
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: {
    tasks: Array,
  },
};
</script>

<style lang="sass" scoped>
.bounce-enter-active
  animation: bounce-in 0.7s

.bounce-leave-active
  animation: bounce-in 0.5s reverse

@keyframes bounce-in
  0%
    transform: scale(0)

  50%
    transform: scale(1.05)

  100%
    transform: scale(1)
</style>
