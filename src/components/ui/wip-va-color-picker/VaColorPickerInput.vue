<template>
  <div class="va-color-picker-input">
    <div v-if="validator(this.mode)">
      <va-dropdown fixed>
        <div
          class="va-color-picker-input__slot"
        >
          <slot>
            <va-color-input
              v-model="valueProxy"
              mode="palette"
              :disabled="isInputDisabled"
              :selected="selected"
            />
          </slot>
        </div>
        <div class="va-color-picker-input__dropdown">
          <va-advanced-color-picker
            v-if="this.mode === 'advanced'"
            v-model="valueProxy"
          />
          <va-simple-palette-picker
            v-if="this.mode === 'palette'"
            v-model="valueProxy"
            :palette="palette"
          />
          <va-slider-color-picker
            v-if="this.mode === 'slider'"
            v-model="valueProxy"
          />
        </div>
      </va-dropdown>
    </div>
    <div v-else>
      <slot>
        <va-color-input
          v-model="valueProxy"
          mode="palette"
          :disabled="isInputDisabled"
        />
      </slot>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import {
  VaAdvancedColorPicker,
  VaSimplePalettePicker,
  VaSliderColorPicker,
} from './index'

export default defineComponent({
  name: 'VaColorPickerInput',
  components: {
    VaSimplePalettePicker,
    VaAdvancedColorPicker,
    VaSliderColorPicker,
  },
  props: {
    modelValue: {
      type: String,
      default: '',
    },
    mode: {
      type: String,
      default: '',
    },
    palette: {
      type: Array,
      default: () => [],
    },
    selected: {
      type: Boolean,
      default: false,
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

    const isInputDisabled = (): boolean => {
      return !!(props.mode === 'palette' && props.palette)
    }

    const validator = (value: string): boolean => {
      return ['palette', 'slider', 'advanced'].includes(value)
    }

    return {
      valueProxy,
      isInputDisabled,
      validator,
    }
  },
})
</script>

<style lang="scss">
// @import "../../../sass/main.scss";

.va-color-picker-input {
  &__dropdown {
    // background: var(--va-white);
    background: white;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  }

  &__slot {
    cursor: pointer;
  }
}
</style>
