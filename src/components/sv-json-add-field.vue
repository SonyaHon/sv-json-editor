<template>
  <div class="sv-add-field">
    <div class="activator" v-if="!active">
      <v-btn @click="active = true" class="very-small" small icon>
        <v-icon size="16">mdi-plus</v-icon>
      </v-btn>
    </div>
    <div class="from" v-else>
      <input class="value-content" type="text" v-model="key" v-if="!isArray" />
      <div class="value-content" v-else>{{ suggestedKey }}</div>

      <select class="value-content" v-model="type">
        <option value="boolean">Boolean</option>
        <option value="string">String</option>
        <option value="number">Number</option>
        <option value="object">Object</option>
        <option value="array">Array</option>
      </select>

      <div v-if="type !== ''">
        <input
          class="value-content"
          type="text"
          v-model="value"
          v-if="type === 'string'"
        />
        <input
          class="value-content"
          type="number"
          v-model="value"
          v-if="type === 'number'"
        />
        <select class="value-content" v-if="type === 'boolean'" v-model="value">
          <option :value="true">True</option>
          <option :value="false">False</option>
        </select>
        <span v-if="type === 'object'">{}</span>
        <span v-if="type === 'array'">[]</span>
      </div>
      <v-btn @click="appendField" class="very-small" small icon>
        <v-icon size="16">mdi-check</v-icon>
      </v-btn>

      <v-btn @click="active = false" class="very-small" small icon>
        <v-icon size="16">close</v-icon>
      </v-btn>
    </div>
  </div>
</template>

<script>
export default {
  name: "sv-json-add-field",
  props: ["isArray", "suggestedKey"],
  watch: {
    type(val) {
      if (val === "string") this.value = "";
      if (val === "number") this.value = 0;
      if (val === "boolean") this.value = false;
      if (val === "object") this.value = {};
      if (val === "array") this.value = [];
    }
  },
  data() {
    return {
      active: false,
      key: "",
      type: "string",
      value: ""
    };
  },
  methods: {
    appendField() {
      this.$emit("append-field", {
        key: this.key,
        type: this.type,
        value: this.value
      });
      this.active = false;
    }
  }
};
</script>

<style scoped>
.sv-add-field {
  display: flex;
  justify-content: flex-start;
}
.very-small {
  width: 20px !important;
  height: 20px !important;
}
.from {
  display: flex;
  align-items: center;
}
.value-content {
  border-bottom: 1px solid lightskyblue;
  height: 1.5em;
  margin-right: 8px;
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
