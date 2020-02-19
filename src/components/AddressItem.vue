<template>
  <div class="address-item">
    <div class="address-item__check">
      <label :for="'check' + address.id" class="radio">
        <input
          type="radio"
          name="selected-address"
          :id="'check' + address.id"
          :checked="address.active"
          class="radio__input"
          @change="$emit('set-active-address', address.id)"
        />
        <span class="radio__span"></span>
      </label>
    </div>
    <div class="address-item__address" v-if="!editMode">
      <label :for="'check' + address.id" class="address-item__address-line">
        {{ address.value }}
      </label>
    </div>
    <div class="address-item__address" v-if="editMode">
      <input
        type="text"
        v-model="address.value"
        class="input input_full input_sm"
      />
    </div>
    <div class="address-item__button" v-if="editMode">
      <button
        class="button-link button-link_orange"
        @click.prevent="$emit('remove-address', address.id)"
      >
        удалить
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["address", "editMode"]
};
</script>
