<template>
  <div class="w-full mx-auto text-center py-5" >
    <BreadCrumles/>
    <div class="mt-5" v-if="subject.questions.length">
      <Question v-if="subject?.questions?.length > 0 && showNextQuestion"
                @on-answer-selected="answerSelected"
                @on-next-question="nextQuestion"
                :question="subject.questions[count]"
                :q-index="count + 1"
                :count="subject.questions.length"
                :buttonText="buttonText"
      />
      <Result v-else :score="score" :correctAnswers="subject.correctAnswers"/>
    </div>
    <h2 class="mt-5" v-else>The questions will be added soon.</h2>
  </div>
</template>

<script setup lang="ts">
import subjectMap from "~/utils/subjectMap";
import Result from "~/components/result.vue";
interface IQuestion {
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
const buttonText = ref('next');
const score = ref(0);
const showNextQuestion = ref(true)

const subject:Ref<ISubject>  = ref({
  title: '',
  correctAnswers: 0,
  questions: []
})

const answerSelected = (index: number) => {
  if (subject.value.questions[count.value].selected_answer !== null) return false;
  if (count.value + 1 === subject.value.questions.length) {
    buttonText.value = 'show results'
  }
  subject.value.questions[count.value] = {
    ...subject.value.questions[count.value],
    selected_answer: index
  };

  if (index === subject.value.questions[count.value].correct_answer) {
    subject.value.correctAnswers += 1
  }
}

const nextQuestion = () => {
  if (count.value + 1 === subject.value.questions.length) {
    showNextQuestion.value = false;
    score.value = 100 * subject.value.correctAnswers / subject.value.questions.length;

    return;
  } else {
    count.value += 1;
  }
}

onMounted(() => {
  const subjectTitle = route.params.name;
  const properSubjectObject = subjectMap.find(subject => subject.title === subjectTitle);
  if (properSubjectObject) {
    const { title, questions } = properSubjectObject;
    subject.value.title = title;
    subject.value.questions = questions as IQuestion[];
  }
})
</script>



<style scoped>

</style>