<template>
  <div class="bg-gray-900 text-amber-50 h-full">
    <navbar />
    <main>
      <router-view/>
    </main>
  </div>
</template>

<script setup>
import Navbar from "./Navbar.vue";
</script>