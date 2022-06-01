<template>
  <header class="bg-slate-700 text-center py-3">
    <router-link to="/">
      <h1 class="text-4xl font-medium text-white">
        <span class="text-green-500">Vue</span>Movies
      </h1>
    </router-link>
  </header>
  <router-view />
</template>

<script>
export default {};
</script>

<style>
#app {
  min-height: 100vh;
  background-color: #0f172a;
}
</style>
