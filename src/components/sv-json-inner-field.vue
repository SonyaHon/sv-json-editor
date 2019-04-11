<template>
  <div class="field">
    <div class="label">
      <div
        class="label-content"
        contenteditable
        @input="changePropName($event.target.innerText)"
      >
        {{ propName }}
      </div>
      <div class="separator">:</div>
      <sv-json-value-string
        v-if="type === 'string'"
        :value="value"
      ></sv-json-value-string>
      <sv-json-value-number
        v-if="type === 'number'"
        :value="value"
      ></sv-json-value-number>
      <sv-json-value-bool v-if="type === 'boolean'" :value="value">
      </sv-json-value-bool>
      <sv-json-value-object
        v-if="type === 'object'"
        :value="value"
      ></sv-json-value-object>
    </div>
  </div>
</template>

<script>
import events from "../events";
import SvJsonValueString from "./sv-json-value-string.vue";
import SvJsonValueNumber from "./sv-json-value-number";
import SvJsonValueBool from "./sv-json-value-bool";
import SvJsonValueObject from "./sv-json-value-object";

export default {
  name: "sv-json-inner-field",
  props: ["propName", "value"],
  components: {
    SvJsonValueString,
    SvJsonValueNumber,
    SvJsonValueBool,
    SvJsonValueObject
  },
  computed: {
    type() {
      if (typeof this.value !== "object") return typeof this.value;
      return Array.isArray(this.value) ? "array" : "object";
    }
  },
  methods: {
    changePropName(newName) {
      console.log(newName);
    }
  }
};
</script>

<style scoped>
.field {
  width: 100%;
  display: flex;
  flex-direction: column;
}
.label {
  width: 100%;
  display: flex;
  margin: 4px 0;
}
.label-content {
  margin: 0 4px;
}
.label-content:active {
  outline: 0 solid transparent;
  border: none;
  box-shadow: none;
  background-color: lightgoldenrodyellow;
  text-decoration: none;
}
.label-content:focus {
  outline: 0 solid transparent;
  border: none;
  box-shadow: none;
  background-color: lightgoldenrodyellow;
  text-decoration: none;
}
.separator {
  margin-left: 2px;
  margin-right: 4px;
}
</style>
