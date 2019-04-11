<template>
  <div class="value">
    <div class="info">
      <span class="info-text">[ {{ value.length }} ]</span>
      <v-btn small icon @click="opened = !opened">
        <v-icon v-if="!opened">mdi-chevron-right</v-icon>
        <v-icon v-if="opened">mdi-chevron-down</v-icon>
      </v-btn>
    </div>
    <div class="content" v-if="opened">
      <sv-json-field
        v-for="(field, key) in value"
        :key="key"
        :prop-name="key"
        :value.sync="value[key]"
        :key-editable="false"
      ></sv-json-field>
      <sv-add-field
        :is-array="true"
        :suggested-key="value.length"
        @append-field="appendField"
      ></sv-add-field>
    </div>
  </div>
</template>

<script>
import SvJsonField from "./sv-json-field";
import SvAddField from "./sv-json-add-field";
export default {
  name: "sv-json-value-object",
  components: { SvJsonField, SvAddField },
  props: ["value"],
  data() {
    return {
      opened: false
    };
  },
  methods: {
    appendField(f) {
      let val = [
        ...this.value,
        f.type === "number" ? Number(f.value) : f.value
      ];
      this.$emit("update", val);
    }
  }
};
</script>

<style scoped>
.value {
  width: 100%;
  margin: 1px;
}
.info {
  width: 100%;
  display: flex;
  align-items: center;
  height: 1.5em;
}
.info-text {
  color: lightskyblue;
}
.content {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: flex-start;
}
</style>
