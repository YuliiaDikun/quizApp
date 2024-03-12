<script setup lang="ts">
interface IQuestion  {
  title: string
  correct_answer: number
  selected_answer: null | number
  answers: string[]
}
defineProps({
  'question': {
    type: Object as PropType<IQuestion>,
    required:true
  },
  'count': {
    type:Number,
    required:true
  },
  'qIndex':{
    type:Number,
    required:true
  },
  'buttonText':{
    type: String,
    required:true
  }
});
const emit = defineEmits(['onAnswerSelected', 'onNextQuestion']);

const onAnswerClick = (index: string | number) => {
  emit('onAnswerSelected', Number(index));
}
</script>

<template>

<div class="bg-gray-200 dark:bg-blue-900 rounded p-5 max-w-[300px] mx-auto relative" >
  <span class="text-xs absolute top-2 right-1" >{{qIndex}} / {{count}}</span>
  <h2 class="my-3 text-base md:text-xl md:mb-5">{{question.title}}</h2>
  <button
      v-for="(answer, index) in question.answers"
      :key="`answer-${index}`"
      @click="onAnswerClick(index)"
      :class="{'bg-green-400 text-white' : question.selected_answer !== null && index === question.correct_answer},
       {'bg-red-400 text-white' : question.selected_answer !== question.correct_answer && index === question.selected_answer},
       {'bg-white dark:bg-blue-950 ' : question.selected_answer === null}
        "
      class="cursor-pointer px-2 py-1 hover:bg-blue-200 dark:hover:bg-blue-800 transition-colors rounded mb-3 w-full">
      {{ answer }}
  </button>

  <button @click="emit('onNextQuestion')" v-show="question.selected_answer !== null"  class="block ml-0 w-content px-2 py-1 bg-blue-700 text-white text-white text-sm rounded">{{buttonText}}</button>
</div>
</template>

<style scoped>

</style>