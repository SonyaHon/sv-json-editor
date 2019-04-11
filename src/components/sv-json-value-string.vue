<template>
  <div class="value">
    <div class="value-type">(String)</div>
    <input
      style="width: 100%;"
      type="text"
      class="value-content"
      v-model="model"
    />
  </div>
</template>

<script>
export default {
  name: "sv-json-value-string",
  props: ["value"],
  data() {
    return {
      model: ""
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
