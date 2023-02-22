<template>
  <header class="navbar bg-light">
    <div class="container-fluid">
      <!-- navbar brand -->
      <nuxt-link tag="a" class="navbar-brand text-brand" to="/">
        <img
          src="/images/logo.png"
          alt="Image of Recipe App Logo"
          width="44"
          height="44"
          class="d-inline-block align-text-center"
        />
        Food Recipes
      </nuxt-link>
      <!-- !navbar brand -->

      <!-- navbar list -->
      <ul class="nav justify-content-end">
        <li class="nav-item">
            <nuxt-link to="/" class="nav-link active" aria-current="page" >Home</nuxt-link>
        </li>
        <li class="nav-item">
            <nuxt-link to="/add" class="nav-link">Add Recipes</nuxt-link>
        </li>
        <li class="nav-item" v-if="!$store.getters.isAuth">
            <nuxt-link  to="/user/login" class="nav-link">Login</nuxt-link>
        </li>
        <li class="nav-item" v-if="$store.getters.isAuth">
            <nuxt-link to="/user" class="nav-link" >{{ $store.state.userData.username }}</nuxt-link>
        </li>
        <li class="nav-item" v-if="$store.getters.isAuth">
            <a class="nav-link" @click.prevent="logout">Logout</a>
        </li>
      </ul>
      <!-- !navbar list -->
    </div>
  </header>
</template>

<script>
export default {
  methods: {
    logout() {
      this.$store.dispatch("logout");

      this.$router.push("/user/login");
    },
  },
};
</script>

<style>
header {
    margin-bottom: 20px;
}

a:hover {
    cursor: pointer;
}

.text-brand {
  font-family: 'Satisfy', cursive;
}
</style>
