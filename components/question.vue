<script setup lang="ts">
const props = defineProps(['question', 'count', 'qIndex', 'buttonText']);
const emit = defineEmits(['onAnswerSelected', 'onNextQuestion']);

const onAnswerClick = (index: string | number) => {
  emit('onAnswerSelected', Number(index));
}
</script>

<template>

<div class="bg-gray-200 rounded p-3 max-w-[250px] mx-auto relative" >
  <span class="text-xs absolute top-1 right-1" >{{qIndex}} / {{count}}</span>
<h2 class="mb-3 text-xl">{{question.title}}</h2>

  <button
      v-for="(answer, index) in question.answers"
      :key="`answer-${index}`"
      @click="onAnswerClick(index)"
      :class="{'bg-green-400 text-white' : question.selected_answer !== null && index === question.correct_answer},
       {'bg-red-400 text-white' : question.selected_answer !== question.correct_answer && index === question.selected_answer},
       {'bg-white' : question.selected_answer === null}
        "
      class="cursor-pointer px-2 py-1 hover:bg-blue-200 transition-colors rounded mb-3 w-full">
      {{ answer }}
  </button>

  <button @click="emit('onNextQuestion')" v-show="question.selected_answer !== null"  class="block ml-0 w-content px-2 py-1 bg-blue-700 text-white text-white text-sm rounded">{{buttonText}}</button>
</div>
</template>

<style scoped>

</style>