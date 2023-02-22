<template>
  <div v-if="isLoading">Loading...</div>
  <app-recipe-form v-else :recipe="recipeDetail"></app-recipe-form>
</template>

<script>
import RecipeForm from "~/components/admin/RecipeForm.vue";
export default {
  middleware: ["check-auth", "auth"],
  components: {
    "app-recipe-form": RecipeForm,
  },
  data() {
    return {
      isLoading: true,
    };
  },
  async created() {
    await this.$store.dispatch(
      "getRecipeDetail",
      this.$route.params.detail
    );
    if (this.recipeDetail.userId !== this.userId) {
      this.$router.push("/");
    } else {
      this.isLoading = false;
    }
  },
  computed: {
    recipeDetail() {
      return this.$store.state.recipeDetail;
    },
    userId() {
      return this.$store.getters.userId;
    },
  },
};
</script>
