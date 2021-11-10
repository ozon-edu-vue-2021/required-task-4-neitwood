<template>
  <div class="wrapper">
    <div class="caption">{{ caption }}</div>
    <input
      type="text"
      :placeholder="placeholder"
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    />
  </div>
</template>

<script>
export default {
  name: "Input",
  props: {
    caption: String,
    placeholder: String,
    value: String,
  },
};
</script>

<style scoped>
.wrapper {
  margin: 5px;
}
.caption {
  color: #7b7b7b;
  padding-bottom: 5px;
}
</style>
