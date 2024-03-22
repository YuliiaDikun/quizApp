<template>
  <div class="text-center">
    <h2>Your result: {{score}} %</h2>
    <p>Correct answers - {{correctAnswers}}.</p>
    <div class=" flex items-center justify-center w-full">
      <img class="shrink-0 -mr-5" :src="Penguine" alt="penguin icon">
      <div class="comment-text relative mt-3 text-center w-fit bg-blue-950 dark:bg-gray-300 rounded px-3 py-5 text-white dark:text-blue-950">{{resultFinalMessage[score].title}} </div>
    </div>

  </div>
</template>

<script setup lang="ts">
import Penguine from '~/assets/icons/penguin-svgrepo-com.svg';
import resultFinalMessage from "~/utils/constants";

interface Props {
  score: number,
  correctAnswers:number
}

defineProps<Props>()

</script>

<style scoped>
.comment-text::before {
  position: absolute;
  content: '';
  top: 8%;
  left: -1px;
  width: 2.7%;
  padding-bottom: 2.5%;
  background: inherit;
  border-style: solid;
  border-width: 1px 0 0 1px;
  border-color: inherit;
  transform-origin: 50% 0;
  transform: translateX(-100%) skewX(45deg);
  z-index: 1;
}
</style>