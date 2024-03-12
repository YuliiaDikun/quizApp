<template>
<ul class="w-full uppercase flex items-center justify-start gap-2 text-xs text-blue-950 dark:text-gray-200">
  <NuxtLink to="/">Home</NuxtLink>
  <span>-</span>
  <p class="text-blue-400 dark:text-gray-400">{{pageTitle}}</p>
</ul>
</template>

<script setup lang="ts">
const route = useRoute();
const pageTitle:Ref<string> = ref('');

onMounted(() => {
    pageTitle.value = route.params.name as string;
  }
)
</script>

<style scoped>

</style>