<template>
  <button class="btn" :color="color" @click="$emit('action')">
    <slot />
  </button>
</template>

<script>
export default {
  emits: ['action'],
  props: {
    color: {
      type: String,
      default: '',
      validator(colorValue) {
        return ['', 'danger', 'primary'].includes(colorValue)
      },
    },
  },
}
</script>
