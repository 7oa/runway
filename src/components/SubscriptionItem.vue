<template>
  <div class="subscription-item">
    <input
      type="checkbox"
      :id="'subscription-item' + subscription.id"
      @change="subscription.active = !subscription.active"
      :checked="subscription.active"
      class="subscription-item__input checkbox"
    />
    <label
      :for="'subscription-item' + subscription.id"
      class="subscription-item__label"
      >{{ subscription.value }}</label
    >
  </div>
</template>

<script>
export default {
  props: ["subscription"]
};
</script>
