<template>
  <div>
    <app-recipe-list :isUser="true" :recipeList="recipes"></app-recipe-list>
  </div>
</template>
<script>

import RecipeList from "../../components/recipe/RecipeList.vue";

export default {
  middleware: ['check-auth', 'auth'],
  components: {
    "app-recipe-list": RecipeList,
  },
  async created() {
    await this.$store.dispatch("getRecipeList");
  },
  computed: {
    recipes() {
      const userId = this.$store.getters.userId;
      const recipes = this.$store.getters.recipesData;

      console.log(recipes);

      return recipes.filter((recipe) => recipe.userId === userId)
    },
  },
};
</script>
