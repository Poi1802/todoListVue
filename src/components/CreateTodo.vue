<template>
  <div class="todo__create flex flex-col w-96 relative mx-auto py-6">
    <label class="text-slate-200" for="start">Deadline:</label>
    <input
      v-model="deadline"
      class="rounded-lg p-1 mb-4"
      type="date"
      id="start"
      name="trip-start"
      min="2023-03-11"
      max="2025-03-11" />

    <input
      v-model="task"
      @keydown.enter="$emit('pressEnter', task, deadline), (task = '')"
      type="text"
      class="create__title w-full p-2 font-semibold"
      placeholder="Your task" />
    <div
      @click="$emit('clickAdd', task, deadline), (task = '')"
      class="create-btn active:scale-110 duration-150 bg-emerald-500 w-fit cursor-pointer">
      <i class="create-plus p-2 fa-solid fa-plus"> </i>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: '',
      deadline: '',
    };
  },
};
</script>

<style lang="sass" scoped></style>
