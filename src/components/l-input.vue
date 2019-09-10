<template>
  <div>
    {{someval}}
    <input :type="type"  :value="value"  @input="onInput">
    <br> >
  </div>
</template>

<script>
  export default {
    // 跨级通信
    inject: ['someval'],
    props:{
      value: {
        type: String,
        default: ''
      },
      type: {
        type: String,
        default: 'text'
      }
    },
    methods: {
      //  双向绑定-v-model——绑定value值和监听input事件
      onInput(e) {
        let value = e.target.value;
        this.$emit('input', value)
        // $parent-父级的实例， 组件component
        this.$parent.$emit('validate')
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>