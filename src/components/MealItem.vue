<template>
  <div class="bg-gray-800 shadow rounded-xl">
    <div class="p-3">
      <router-link :to="{name: 'mealDetails', params:{id:meal.idMeal}}">
        <img :src="meal.strMealThumb" :alt="meal.strMeal" class="rounded-t-xl h-48 object-cover w-full">
      </router-link>
      <h3 class="font-bold">{{ meal.strMeal }}</h3>
      <p class="mb-4">
        {{meal.strTags}}
      </p>
      <div>
        <YoutubeButton :href="meal.strYoutube">Youtube</YoutubeButton>

      </div>
    </div>
  </div>
</template>
<script setup>
import YoutubeButton from "./YoutubeButton.vue";
const {meal} = defineProps({
  meal: {
    required: true,
    type: Object
  }
})
</script>