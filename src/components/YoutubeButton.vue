<template>
  <a :href="href" target="_blank"
     class="my-2 px-3 py-2 rounded border-2 border-red-500 bg-red-500 hover:bg-red-600 transition-colors hover:cursor-pointer">
    <slot></slot>
  </a>
</template>

<script setup>
const props = defineProps({
  href: String
})
</script>