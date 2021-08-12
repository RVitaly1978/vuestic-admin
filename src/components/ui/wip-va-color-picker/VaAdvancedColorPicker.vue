<template>
  <ChromePicker
    v-model="valueProxy"
    class="va-advanced-color-picker"
  />
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { Chrome } from 'vue-color'

export default defineComponent({
  name: 'VaAdvancedColorPicker',
  components: {
    ChromePicker: Chrome,
  },
  props: {
    modelValue: {
      type: String,
      default: '',
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

    return {
      valueProxy,
    }
  },
})
</script>

<style lang="scss">
.va-advanced-color-picker {
  .vc-chrome-alpha-wrap {
    display: none;
  }

  .vc-chrome-hue-wrap {
    margin-top: 10px;
  }

  .vc-chrome-toggle-btn {
    display: none;
  }
}
</style>
