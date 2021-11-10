<template>
  <div class="wrapper">
    <input
      type="radio"
      :id="id"
      :name="name"
      :value="label"
      v-model="radioButtonValue"
    />
    <label :for="id">{{ label }}</label>
  </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    id: String,
    name: String,
    value: String,
    label: String,
  },
  computed: {
    radioButtonValue: {
      get: function () {
        return this.value;
      },
      set: function () {
        // Communicate the change to parent component so that selectedValue can be updated
        this.$emit("change", this.label);
      },
    },
  },
};
</script>

<style scoped>
.wrapper {
  margin: 5px;
  display: flex;
  flex-direction: row;
}
</style>
