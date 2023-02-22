<template>
  <div class="col-4">
    <!-- add -->
    <button
      v-if="buttonType === 'add'"
      type="button"
      class="btn btn-success"
      v-on="$listeners"
    >
      <slot></slot>
    </button>

    <!-- delete -->
    <button v-else type="button" class="btn btn-danger" v-on="$listeners">
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    buttonType: {
      type: String,
      default: "add",
    },
  },
};
</script>
