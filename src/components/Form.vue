<template>
  <div>
    <form action="">
      <slot></slot>
    </form>
  </div>
</template>

<script>
  export default {
    provide() {
      return {
        lForm: this   // 把form.vue自己作为实例传出去
      }
    },
    props: {
      model: {
        type: Object,
        required: true
      },
      rules: {
        type: Object
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>