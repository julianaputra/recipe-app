<template>
  <div class="mb-3">
    <slot></slot>
    <textarea
      @input="$emit('input', $event.target.value)"
      :value="value"
      class="form-control"
      rows="4"
    ></textarea>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: "",
    },
  },
};
</script>
