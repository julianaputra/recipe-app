<template>
  <div class="col-md-6 col-lg-3">
    <div class="card">
      <img
        class="recipes-content__img card-img-top rounded"
        alt="Pasta"
        :src="detail.recipeImage"
      />
      <div class="card-body">
        <p class="card-username">{{ detail.username }}</p>
        <nuxt-link
          class="card-text fs-5 text"
          style="height: 45px; align-item: center"
          :to="{ name: 'recipe-detail', params: { detail: detail.id } }"
          tag="h1"
        >
          {{ detail.recipeTitle }}
        </nuxt-link>
        <div class="recipes-content__body__review card-footer bg-transparent row">
          <div class="col-2">
            <img :src="likeImage" alt="Heart" @click="onLike" />
          </div>
          <div class="col-6">
            <p>{{ likeCount }} likes</p>
          </div>
          <div v-show="isUser" class="col-2">
            <img src="images/delete.svg" alt="Delete" @click="deleteRecipe" />
          </div>
          <div v-show="isUser" class="col-2">
            <img src="images/edit.svg" alt="Edit" @click="editRecipe" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    detail: {
      type: Object,
      default: ""
    },
    isUser: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    likeCount() {
      if (this.detail.dataLikes.length === 1) {
        if (this.detail.dataLikes[0] === "null") {
          return 0;
        } else {
          return 1;
        }
      } else {
        return this.detail.dataLikes.length;
      }
    },
    likeImage() {
      const checkLike = this.detail.dataLikes.find((user) => {
        return user === this.userEmail;
      });

      if (checkLike) {
        return "images/heart-red.png";
      } else {
        return "images/heart-black.png";
      }
    },
    userEmail() {
      return this.$store.getters.userEmail;
    },
  },
  methods: {
    async onLike() {
      if (!this.$store.getters.isAuth) {
        this.$router.push("/user/login");
      }

      const userEmail = this.userEmail;
      const recipe = JSON.parse(JSON.stringify(this.detail));

      if (recipe.dataLikes.length === 1 && recipe.dataLikes[0] === "null") {
        recipe.dataLikes[0] = userEmail;
      } else {
        const checkLike = recipe.dataLikes.find((email) => {
          return email === userEmail
        })

        if (!checkLike) {
          recipe.dataLikes.push(userEmail)
        } else {

          if (recipe.dataLikes.length === 1) {
              recipe.dataLikes[0] = "null"
          } else {
            const userIndex = recipe.dataLikes.findIndex((email) => {
              return email === userEmail
            })
            
            recipe.dataLikes.splice(userIndex, 1)
          }
        }
      }

      let { id:_, ...newRecipe } = recipe

      await this.$store.dispatch('updateLike', {
        recipeId: this.detail.id,
        newDataRecipe: newRecipe
      })

      await this.$store.dispatch('getRecipeList');
    },
    deleteRecipe() {
      this.$store.dispatch('deleteRecipe', this.detail.id)
    },
    editRecipe() {
      this.$router.push("/recipe/" + this.detail.id + "/edit")
    }
  },
};
</script>

<style>
/* Recipe Content */
.recipes-content {
  background-color: #eef2e6;
  padding: 10px;
  margin: 13px 13px;
}

.recipes-content__body {
  padding: 5px;
}

.recipes-content__img {
  width: 100%;
  height: 25vh;
}

.recipes-content__body__review {
  display: flex;
  align-items: center;
}

.recipes-content__body__review img {
  width: 20px;
  height: 20px;
  margin: 5px 10px 5px 0px;
}

.recipes-content__body__review p {
  margin: 0px;
}

.recipes-content__body__review img:hover {
  cursor: pointer;
}

.recipes-content__body__title {
  margin: 5px 0px;
}

.card-username {
  margin-bottom: 0;
}
</style>
