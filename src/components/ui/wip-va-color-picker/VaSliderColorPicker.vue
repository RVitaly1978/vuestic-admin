<template>
  <SliderPicker
    v-model="valueProxy"
    class="vuestic-slider-picker"
  />
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { Slider } from 'vue-color'

export default defineComponent({
  name: 'VaColorPickerInput',
  components: {
    SliderPicker: Slider,
  },
  props: {
    modelValue: {
      type: String,
      default: '',
    }
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

    return {
      valueProxy,
    }
  },
})
</script>

<style>
.vuestic-slider-picker {
  max-width: 100%;
  padding: 8px;
}
</style>
