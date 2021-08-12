<template>
  <div
    class="color-dot"
    @click="$emit('click')"
    :class="{'color-dot--selected': selected}"
  >
    <div
      class="color-dot__core"
      :style="{'background-color': color}"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ColorDot',
  emits: ['click'],
  props: {
    color: {
      type: String,
      default: '',
    },
    selected: {
      type: Boolean,
      default: false,
    },
  },
})
</script>

<style lang="scss">
// @import "../../../sass/main.scss";

.color-dot {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 1.5rem;
  height: 1.5rem;
  min-width: 1.5rem;
  cursor: pointer;
  border-radius: 50%;
  text-align: center;
  border: solid 0.125rem transparent;

  &--selected {
    // border-color: var(--va-vue-darkest-blue);
    border-color: darkblue;
  }

  &__core {
    display: inline-block;
    vertical-align: baseline;
    border-radius: 50%;
    width: 1rem;
    height: 1rem;
  }
}
</style>
