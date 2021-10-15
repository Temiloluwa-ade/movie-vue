<template>
  <div class="bg-blue-700">
    <header class="bg-blue-900 flex justify-center">
      <router-link to="/">
        <h1 class="text-white font-bold text-2xl">
          <span class="text-green-600">Vue</span>Movies
        </h1>
      </router-link>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>
