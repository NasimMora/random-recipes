<template>
  <button>
    <template v-if="loading">
      Loading...
    </template>
    <template v-else>
      Click
    </template>

  </button>
</template>

<script>
export default {
  name: "VBtn",
  props: {
    loading: {
      type: Boolean,
      default: false,
    }
  }
}
</script>

<style scoped>

</style>
