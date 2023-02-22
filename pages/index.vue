<template>
    <main>
      <div v-if="isLoading">Loading...</div>
      <app-recipe-list v-else :recipeList="recipes"></app-recipe-list>
    </main>
</template>

<script>
import RecipeList from "~/components/recipe/RecipeList.vue";

export default {
  name: "IndexPage",
  middleware: 'check-auth',
  data() {
    return {
      isLoading: true
    }
  },
  components: {
    "app-recipe-list": RecipeList,
  },
  computed: {
    recipes() {
      return this.$store.getters.recipesData;
    },
  },
  async created() {
    await this.$store.dispatch("getRecipeList");
    this.isLoading = false
  },
};
</script>

<style>
body {
  margin: 0px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-left: 40px;
  padding-right: 40px;
  background-color: #eef2e6;
}

main {
  margin: 22px;
}

.header-nav__link {
  margin-left: 20px;
  color: black;
  text-decoration: none;
  font-size: 20px;
}
</style>
