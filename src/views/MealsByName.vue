<template>
  <div class="p-8">
    <input type="text"
           v-model = "keyword"
           class="rounded border-2 border-gray-200 w-full bg-gray-800"
           placeholder="Search for Meals"
           @change = "searchMeals"
    />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div v-for="meal of meals" :key="meal.idMeal" class="bg-gray-800 shadow rounded-xl">
      <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl h-48 object-cover w-full">
      <h3 class="p-3 font-semibold">{{meal.strMeal}}</h3>
      <div class="p-3">
        <a :href="meals.strYoutube" target="_blank">Youtube</a>
        <router-link to="/">View</router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import {computed, ref} from "vue";
import axios from "axios";
import axiosClient from "../axiosClient.js";
import store from "../store/index.js";

const keyword= ref('')
const meals = computed(() => store.state.searchedMeals);
function searchMeals(){
  store.dispatch('searchMeals', keyword.value)
}
</script>