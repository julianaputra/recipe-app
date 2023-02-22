<template>
  <div v-if="recipeDetail && isLoading === false">
    <main>
      <div class="recipes-detail">
        <div>
          <img
            class="recipes-detail__img"
            alt="Pasta"
            :src="recipeDetail.recipeImage"
          />
          <h1 class="recipes-detail__title">
            {{ recipeDetail.recipeTitle }}
          </h1>
          <p class="recipes-detail__body">
            {{ recipeDetail.body }}
          </p>
        </div>
      </div>
    </main>
  </div>
  <div
    class="text-center d-flex align-items-center justify-content-center"
    style="height: 100vh"
    v-else
  >
    <div class="spinner-border text-primary" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: true,
    };
  },
  async created() {
    await this.$store.dispatch("getRecipeDetail", this.$route.params.detail);
    this.isLoading = false;
  },
  computed: {
    recipeDetail() {
      return this.$store.state.recipeDetail;
    },
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

.recipes {
  display: flex;
  flex-wrap: wrap;
}

.header-nav__link {
  margin-left: 20px;
  color: black;
  text-decoration: none;
  font-size: 20px;
}

/* Detail */
.recipes-detail {
  display: flex;
  justify-content: center;
}

.recipes-detail div {
  width: 600px;
}

.recipes-detail__img {
  width: 400px;
  height: 300px;
  display: block;
  text-align: center;
  margin: 0px auto;
}

.recipes-detail__title {
  text-align: center;
}
</style>
