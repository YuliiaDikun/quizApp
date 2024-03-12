<template>
  <div class="max-w-7xl mx-auto text-center px-5 py-5" >
    <h1 class="text-2xl mb-5 text-gray-200">{{subject.title}}</h1>
    <div v-if="subject.questions.length">
      <Question v-if="subject?.questions?.length > 0 && showNextQuestion"
                @on-answer-selected="answerSelected"
                @on-next-question="nextQuestion"
                :question="subject.questions[count]"
                :q-index="count + 1"
                :count="subject.questions.length"
                :buttonText="buttonText"
      />
      <h2 v-else> your score - {{score}}%</h2>
    </div>
    <h2>The questions will be added soon.</h2>
  </div>
</template>

<script setup lang="ts">
import subjectMap from "~/utils/subjectMap";
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

const route = useRoute();

const count = ref(0);
const buttonText= ref('next');
const score = ref(0);
const showNextQuestion = ref(true)

const subject:Ref<ISubject>  = ref({
  title: '',
  correctAnswers: 0,
  questions: []
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

onMounted(() => {
  const subjectTitle = route.params.name;
  const properSubjectObject = subjectMap.find(subject => subject.title === subjectTitle);
  if(properSubjectObject) {
    subject.value.title = properSubjectObject.title;
    subject.value.questions = [... subject.value.questions, ...properSubjectObject.questions ];
  }
})
</script>



<style scoped>

</style>