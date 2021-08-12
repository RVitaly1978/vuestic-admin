<template>
  <div
    class="va-color-square"
    :style="{'background-color': modelValue}"
  />
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'VaColorSquare',
  props: {
    modelValue: {
      type: String,
      require: true,
    },
  },
})
</script>

<style lang='scss'>
// @import "../../../sass/main.scss";

.va-color-square {
  height: 48px;
  width: 48px;
  border: 1px solid gray;
  // border: 1px solid var(-va-gray-light);
}
</style>
