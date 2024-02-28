<template>
  <div class="p-8 pb-0">
    <input type="text"
           v-model="keyword"
           class="rounded border-2 border-gray-200 w-full bg-gray-800"
           placeholder="Search for Meals"
           @change="searchMeals"
    />
  </div>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <div v-for="meal of meals" :key="meal.idMeal" class="bg-gray-800 shadow rounded-xl">
      <div class="p-3">
       <router-link :to="{name: 'mealDetails', params:{id:meal.idMeal}}">
         <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl h-48 object-cover w-full">
       </router-link>
        <h3 class="font-bold">{{ meal.strMeal }}</h3>
        <p class="mb-4">Lorem</p>
        <div>
          <a :href="meals.strYoutube" target="_blank"
             class="my-2 px-3 py-2 rounded border-2 border-red-500 bg-red-500 hover:bg-red-600 transition-colors hover:cursor-pointer">
            Youtube
          </a>

        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from "vue";
import axios from "axios";
import axiosClient from "../axiosClient.js";
import store from "../store/index.js";
import {useRoute} from "vue-router";

const route = useRoute();
const keyword = ref('');
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch('searchMeals', keyword.value)
}

onMounted(() =>{
  keyword.value = route.params.name
  if(keyword.value){
    searchMeals();
  }
})
</script>