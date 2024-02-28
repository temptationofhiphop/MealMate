<template>
  <div class="w-[700px] mx-auto p-8">
    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
    <img class="w-full rounded-2xl" :src="meal.strMealThumb" :alt="meal.strMeal">
    <div class="grid grid-cols-3 sm:grid-cols-3 text-lg py-2">
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>

      <div>
        <strong class="font-bold">Area:</strong> {{ meal.strArea }}
      </div>

      <div>
        <strong class="font-bold">Tags:</strong> {{ meal.strTags }}
      </div>
    </div>

    <div class="my-3">
      {{meal.strInstructions}}
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-2">Ingredients:</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>

      <div>
        <h2 class="text-2xl font-semibold mb-2">Measures:</h2>

        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strMeasure${ind + 1}`]">
              {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>

    <div class="mt-6">
      <YoutubeButton :href="meal.strYoutube">Youtube</YoutubeButton>
      <a :href="meal.strSource" target="_blank"
         class="my-2 px-3 py-2 rounded border-2 border-blue-500 bg-blue-500 hover:bg-blue-600 transition-colors hover:cursor-pointer">
        View original source
      </a>
    </div>


  </div>

</template>

<script setup>
import {onMounted, ref} from "vue";
import {useRoute} from "vue-router";
import axios from "axios";
import axiosClient from "../axiosClient.js";
import YoutubeButton from "../components/YoutubeButton.vue";

const route = useRoute();
const meal = ref({})

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({data}) => {
      meal.value = data.meals[0] || {}
    })
})
</script>