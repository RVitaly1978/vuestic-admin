<template>
  <ChromePicker
    v-model="valueProxy"
    class="va-color-picker"
  />
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import { Chrome } from 'vue-color'

export default defineComponent({
  name: 'VaColorPicker',
  components: {
    ChromePicker: Chrome,
  },
  props: {
    value: {
      type: String,
      default: '',
    }
  },
  emits: ['input'],

  setup(props, { emit }) {
    const value = ref(props.value)

    const valueProxy = computed({
      get() {
        return value.value
      },
      set(value: string) {
        emit('input', value)
      },
    })

    return {
      valueProxy,
    }
  },
})
</script>

<style lang="scss">
.va-color-picker {
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
