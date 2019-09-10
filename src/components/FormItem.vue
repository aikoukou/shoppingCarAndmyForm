<template>
  <div>
    <label for=""></label>
    <div>
      <slot></slot>
      <p v-if="errStatus">{{errMsg}}</p>
    </div>
  </div>
</template>

<script>
  // 引用类库做校验
  import Schema from 'async-validator'
  export default {
    inject: ['lForm'],
    props: ['label', 'prop'],
    data() {
      return {
        errMsg: '',
        errStatus: false
      }
    },
    mounted() {
      this.$on('validate', this.validator)
    },
    methods: {
      validator() { // 校验规则
        console.log('开始校验！')
        console.log('this.prop',this.prop)
        const rules = this.lForm.rules[this.prop];
        const value = this.lForm.model[this.prop];
        const descriptor = {[this.prop]: rules};
        let schema = new Schema(descriptor);
        // 实例的方法-校验器validate
        // 用户输入 键值对 做校验
        schema.validate({ [this.prop]: value}, errors => {
          if(errors){
            this.errMsg = errors[0].message
            this.errStatus = true;
          } else {
            this.errMsg = ''
            this.errStatus = ''
          }
        })
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>