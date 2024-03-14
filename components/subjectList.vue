<script setup lang="ts">
import subjectMap from '../utils/subjectMap';
</script>

<template>
<ul class="flex items-center justify-center gap-5 flex-wrap">
  <li v-for="link in subjectMap" class="border border-gray-400 rounded-xl px-3 py-2 w-content md:w-[calc((100%-40px)/3)] ">
    <NuxtLink class="uppercase scale-1 text-center block hover:scale-[1.1] transition-transform" :to="'subject/'+link.title">{{link.title}}</NuxtLink>
  </li>
</ul>
</template>

<style scoped>

</style>