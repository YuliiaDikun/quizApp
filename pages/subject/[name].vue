<script setup lang="ts">

interface IQuestion  {
  title: string
  correct_answer: number
  selected_answer: null | number
  answers: string[]
}
interface ISubject {
  title: string
  correctAnswers: number
  questions: IQuestion[]
}
const count = ref(0);
const buttonText= ref('next');
const score = ref(0);
const showNextQuestion = ref(true)

const subject:Ref<ISubject>  = ref({
  title: 'subject title',
  correctAnswers: 0,
  questions: [
    {
      title: 'what is css',
      correct_answer: 0,
      selected_answer: null,
      answers: [
        "web page styling",
        'a car part',
        'sweet cake'
      ]
    },
    {
      title: 'what is html',
      correct_answer: 2,
      selected_answer: null,
      answers: [
        "town",
        'a car part',
        'hyper text markup language'
      ]
    }
  ]
})


const answerSelected = (index:number) => {
  if( subject.value.questions[count.value].selected_answer !== null) return false;
  if(count.value + 1 === subject.value.questions.length) {
    buttonText.value = 'show results'
  }
  subject.value.questions[count.value] = {
    ...subject.value.questions[count.value],
    selected_answer: index
  };

  if (index === subject.value.questions[count.value].correct_answer) {
    subject.value.correctAnswers +=1
  }
}

const nextQuestion = () => {
  if(count.value + 1 === subject.value.questions.length) {

    showNextQuestion.value = false;
    score.value = 100 * subject.value.correctAnswers / Number(subject.value.questions.length);

    return;
  } else {
    count.value +=1;
  }
}
</script>

<template>
  <div class="max-w-7xl mx-auto text-center px-5 py-5">
    <h1 class="text-2xl text-red-500">Quiz App</h1>
    <Question v-if="showNextQuestion"
              @on-answer-selected="answerSelected"
              @on-next-question="nextQuestion"
              :question="subject.questions[count]"
              :q-index="count + 1"
              :count="subject.questions.length"
              :buttonText="buttonText"
    />
    <h2 v-else> your score - {{score}}%</h2>
  </div>
</template>

<style scoped>

</style>