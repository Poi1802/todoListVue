<template>
  <div class="todo__create flex w-96 relative mx-auto py-6">
    <input
      v-model="task"
      @keydown.enter="$emit('pressEnter', task), (task = '')"
      type="text"
      class="create__title w-full p-2 font-semibold"
      placeholder="Your task" />
    <div
      @click="$emit('clickAdd', task), (task = '')"
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
    };
  },
};
</script>

<style lang="sass" scoped></style>
