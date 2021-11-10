<template>
  <div class="wrapper">
    <div class="caption">{{ caption }}</div>
    <select
        v-on:input="$emit('input', $event.target.value)"
    >
      <option
        v-for="option in options"
        v-bind:value="option.value"
        v-bind:key="option.id"
      >
        {{ option.text }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    options: Array,
    caption: String,
    placeholder: String,
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
