<template>
  <div class="va-palette-custom">
    <va-simple-palette-picker
      class="va-palette-custom__palette mr-2"
      :palette="palette"
      v-model="valueProxy"
    />
    <va-color-picker-input
      class="va-palette-custom__input"
      mode="advanced"
      v-model="valueProxy"
    >
      <va-color-input
        :selected="dotIsSelected"
        v-model="valueProxy"
      />
    </va-color-picker-input>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import {
  VaColorPickerInput,
  VaSimplePalettePicker,
} from './index'

export default defineComponent({
  name: 'VaPaletteCustom',
  components: {
    VaColorPickerInput,
    VaSimplePalettePicker,
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
    const value = ref(props.modelValue)

    const valueProxy = computed({
      get() {
        return value.value
      },
      set(value: string) {
        emit('update:modelValue', value)
      },
    })

    const dotIsSelected = (): boolean => {
      return props.palette.includes(valueProxy)
    }

    return {
      valueProxy,
      dotIsSelected,
    } 
  }
})
</script>

<style lang="scss">
.va-palette-custom {
  display: flex;
  align-items: baseline !important;
}
</style>
