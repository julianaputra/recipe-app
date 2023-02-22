<template>
  <div class="container">
    <div v-if="recipeList.length" class="row g-5">
      <app-recipe-item
        v-for="oneRecipe in recipeList"
        :key="oneRecipe.id"
        :detail="oneRecipe"
        :isUser="isUser"
      ></app-recipe-item>
    </div>
    <div v-else>
      <h2 class="text-center text-dark">Recipes not found</h2>
    </div>
  </div>
</template>

<script>
import RecipeItem from "./RecipeItem.vue";

export default {
  components: {
    "app-recipe-item": RecipeItem,
  },
  props: {
    recipeList: {
      type: Array,
      default: ''
    },
    isUser: {
      type: Boolean,
      default: false
    }
  },
};
</script>

<style>
.recipes {
  display: flex;
  flex-wrap: wrap;
}
</style>
