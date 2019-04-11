<template>
  <div class="value">
    <div class="value-type">(Boolean)</div>
    <select v-model="model">
      <option :value="true">True</option>
      <option :value="false">False</option>
    </select>
  </div>
</template>

<script>
export default {
  name: "sv-json-value-bool",
  props: ["value"],
  data() {
    return {
      model: false
    };
  },
  watch: {
    model(newVal) {
      this.$emit("update", newVal);
    }
  },
  mounted() {
    this.model = this.value;
  }
};
</script>

<style scoped>
.value {
  display: flex;
  width: 100%;
}
.value-type {
  margin-right: 4px;
  color: lightskyblue;
}
.value-content {
}
.value-content:active {
  outline: 0 solid transparent;
  border: none;
  box-shadow: none;
  background-color: lightgoldenrodyellow;
  text-decoration: none;
}
.value-content:focus {
  outline: 0 solid transparent;
  border: none;
  box-shadow: none;
  background-color: lightgoldenrodyellow;
  text-decoration: none;
}
</style>
