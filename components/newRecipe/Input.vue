<template>
  <div :class="colStyle">
    <slot></slot>
    <input
      :placeholder="placeholder"
      @input="$emit('input', $event.target.value)"
      :value="value"
      type="text"
      class="form-control"
    />
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: "",
    },
    colStyle: {
      type: String,
      default: "col-12",
    },
    placeholder: {
      type: String,
      default: "",
    },
  },
};
</script>
