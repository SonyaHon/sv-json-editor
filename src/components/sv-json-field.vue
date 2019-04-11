<template>
  <div class="field">
    <div class="label">
      <div
        class="label-content"
        contenteditable
        v-if="keyEditable"
        style="white-space: nowrap;"
        @blur="changePropName($event.target.innerText)"
      >
        {{ propName }}
      </div>
      <div class="label-content no-selection" v-else>{{ propName }}</div>
      <div class="separator">:</div>
      <sv-json-value-string
        v-if="type === 'string'"
        :value="value"
        @update="updateValue"
      ></sv-json-value-string>
      <sv-json-value-number
        v-if="type === 'number'"
        :value="value"
        @update="updateValue"
      ></sv-json-value-number>
      <sv-json-value-bool
        v-if="type === 'boolean'"
        :value="value"
        @update="updateValue"
      >
      </sv-json-value-bool>
      <sv-json-value-object
        v-if="type === 'object'"
        :value="value"
        @update="updateValue"
      ></sv-json-value-object>
      <sv-json-value-array
        v-if="type === 'array'"
        :value="value"
        @update="updateValue"
      ></sv-json-value-array>
    </div>
  </div>
</template>

<script>
import events from "../events";
import SvJsonValueString from "./sv-json-value-string.vue";
import SvJsonValueNumber from "./sv-json-value-number";
import SvJsonValueBool from "./sv-json-value-bool";

export default {
  name: "sv-json-field",
  props: {
    propName: {},
    value: {},
    keyEditable: {
      default: () => true
    }
  },
  components: {
    SvJsonValueString,
    SvJsonValueNumber,
    SvJsonValueBool,
    SvJsonValueObject: () => import("./sv-json-value-object"),
    SvJsonValueArray: () => import("./sv-json-value-array")
  },
  computed: {
    type() {
      if (typeof this.value !== "object") return typeof this.value;
      return Array.isArray(this.value) ? "array" : "object";
    }
  },
  methods: {
    changePropName(newName) {
      this.$emit("update-prop-name", this.propName, newName);
    },
    updateValue(newValue) {
      this.$emit("update:value", newValue);
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
  height: 1.5em;
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
.no-selection {
  user-select: none;
}
</style>
