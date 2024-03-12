<template>
  <div class="text-left">
    <h2>Your result: {{score}} %</h2>
    <p>Correct answers - {{correctAnswers}}.</p>
    <p class="mt-3 text-center w-content bg-blue-950 dark:bg-gray-300 rounded px-3 py-1 mx-auto text-white dark:text-blue-950">{{resultFinalMessage[score].title}} </p>
  </div>
</template>

<script setup lang="ts">
import resultFinalMessage from "~/utils/constants";
defineProps({
  score: {
    type:Number,
    required:true
  },
  correctAnswers: {
    type:Number,
    required:true
  }
})

const finalMessage = ref('')
onMounted(() => {

})
</script>



<style scoped>

</style>