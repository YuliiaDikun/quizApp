<script setup lang="ts">

</script>


  <template>
    <div class="w-full min-h-screen bg-gray-300 dark:bg-blue-950 text-blue-950 dark:text-gray-200">
      <div class=" flex flex-col min-h-screen">
        <header class="h-[50px] py-5 border-b border-blue-950 dark:border-gray-300 flex items-center justify-between">
         <nav class="max-w-7xl mx-auto px-5 md:px-10 w-full">
           <NuxtLink to="/" class="uppercase font-bold text-2xl ml-0">Eng</NuxtLink>
         </nav>

        </header>
        <main class="max-w-7xl w-full mx-auto px-5 md:px-10 grow shrink-0">
        <NuxtPage/>
        </main>
        <footer class=" text-center py-5 border-t border-blue-950 dark:border-gray-300 ">
          <a class="text-sm" href="https://github.com/YuliiaDikun" target="_blank">GitHUB</a>
        </footer>
      </div>
    </div>
  </template>



