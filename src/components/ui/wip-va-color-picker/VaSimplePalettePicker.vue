<template>
  <div class="va-simple-palette-picker">
    <ul class="va-simple-palette-picker__colors">
      <color-dot
        v-for="(color, index) in palette"
        :key="index"
        :color="color"
        @click="handlerClick(color)"
        :selected="isSelected(color)"
      />
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, ref } from 'vue'
import { ColorDot } from './index'

export default defineComponent({
  name: 'VaSimplePalettePicker',
  components: {
    ColorDot,
  },
  props: {
    modelValue: {
      type: String,
      default: '',
    },
    palette: {
      type: Array,
      default: () => [],
    },
  },
  emits: ['update:modelValue'],

  setup(props, { emit }) {
    const valueProxy = ref(props.modelValue)

    const isSelected = computed((color: string): boolean => {
      return valueProxy.value === color
    })

    const handlerClick = (color: string): void => {
      emit('update:modelValue', color)
    }

    return {
      isSelected,
      handlerClick,
    }
  },
})
</script>

<style lang="scss">
.va-simple-palette-picker {
  padding-top: 3px;

  &__colors {
    padding: 3px;
    display: flex;
  }
}
</style>
