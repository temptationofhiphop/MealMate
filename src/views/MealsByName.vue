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
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal"/>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from "vue";
import axios from "axios";
import axiosClient from "../axiosClient.js";
import store from "../store/index.js";
import {useRoute} from "vue-router";
import YoutubeButton from "../components/YoutubeButton.vue";
import MealItem from "../components/MealItem.vue";

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