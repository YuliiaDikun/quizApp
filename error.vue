<script lang="ts" setup>
import Bear from '~/assets/icons/polar-bear-svgrepo-com.svg';
type NuxtError = {
  statusCode: number,
  fatal: boolean,
  unhandled: boolean,
  statusMessage?: string,
  data?: unknown,
  cause?: unknown,
}

defineProps<{
  error: NuxtError
}>()
const handleError = () => clearError({ redirect: '/' })
</script>

<template>
  <div class=" bg-gray-300 dark:bg-blue-950 text-blue-950 dark:text-gray-200">
    <div class="pt-[10%] h-screen w-screen flex flex-col md:flex-row items-center justify-start md:items-start md:justify-center">
     <div>
       <h1 class="mt-6 text-center text-2xl font-light uppercase text-mainColor">{{ error.statusCode }}. {{error.statusMessage}}</h1>
       <button type="button" aria-label="go back to the home page" class="mt-6 min-h-[40px] w-[180px] text-xl font-light mx-auto border border-mainColor flex items-center justify-center px-3 pt-1 pb-2 text-mainColor" @click="handleError">Go back</button>
     </div>
      <img class="shrink-0" :src="Bear" alt="bear icon">
    </div>

  </div>
</template>
