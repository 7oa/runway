<template>
  <div class="field">
    <div class="field__content field__content_saved" v-if="!change">
      <div class="field__saved-value">
        <span v-if="field.value" class="value-set">
          {{ showValue(field.value) }}
        </span>
        <span v-else class="field__placeholder">{{ field.label }}</span>
      </div>
      <div class="field__button">
        <button
          class="button-link button-link_gray"
          @click.prevent="changeValue"
        >
          Изменить
        </button>
      </div>
    </div>
    <div class="field__content field__content_change" v-else>
      <div class="field__input-wrapper">
        <input
          class="input"
          :type="field.type"
          :placeholder="field.placeholder || field.label"
          v-mask="field.pattern"
          v-model="field.value"
        />
      </div>
      <div class="field__button">
        <button
          class="button-link button-link_orange"
          @click.prevent="saveValue"
        >
          Сохранить
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { mask } from "vue-the-mask";

export default {
  directives: { mask },
  data() {
    return {
      change: false
    };
  },
  props: ["field"],
  methods: {
    saveValue() {
      this.change = false;
    },
    changeValue() {
      this.change = true;
    },
    showValue(value) {
      return this.field.type === "password" ? "*".repeat(value.length) : value;
    }
  },
  filters: {
    passwordView(value) {
      return "*".repeat(value.length);
    }
  }
};
</script>
