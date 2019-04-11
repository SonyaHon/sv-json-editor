<template>
  <div class="sv-json-editor">
    <div class="editor-file-title">{{ name }}:</div>
    <div class="editor-content">
      <sv-json-field
        v-for="(field, key) in value"
        :key="key"
        :prop-name="key"
        :value.sync="value[key]"
        @update-prop-name="updatePropName"
      ></sv-json-field>
      <sv-add-field @append-field="appendField"></sv-add-field>
    </div>
  </div>
</template>

<script>
import SvJsonField from "./sv-json-field";
import SvAddField from "./sv-json-add-field";

export default {
  name: "sv-json-editor",
  components: { SvJsonField, SvAddField },
  props: {
    value: {},
    name: {
      default: () => "root"
    }
  },
  data() {
    return {};
  },
  methods: {
    appendField(f) {
      let val = {
        ...this.value,
        [f.key]: f.type === "number" ? Number(f.value) : f.value
      };
      this.$emit("input", val);
    },
    updatePropName(oldName, newName) {
      let val = {};
      for (let key in this.value) {
        if (key !== oldName) {
          val[key] = this.value[key];
        } else {
          val[newName] = this.value[key];
        }
      }
      this.$emit("input", val);
    }
  },
  mounted() {}
};
</script>

<style lang="scss" scoped>
.sv-json-editor {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.editor-file-title {
  display: flex;
  font-size: 18px;
}
.editor-content {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  overflow-y: auto;
}
</style>
