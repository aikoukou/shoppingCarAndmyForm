<template>
  <div>
    <h2>购物车</h2>

    <table>
      <tr>
        <th>勾选</th>
        <th>名称</th>
        <th>单价</th>
        <th>数量</th>
        <th>总价</th>
      </tr>
      <tr v-for="(item,index) in shopListItem" :key="item.id">
        <td>
          <input type="checkbox" v-model="item.isActive" />
        </td>
        <td>{{item.name}}</td>
        <td>{{item.price}}</td>
        <td>
          <button @click="reduce(index)">-</button>
          {{item.num}}
          <button @click="add(index)">+</button>
        </td>
        <td>{{item.price*item.num}}</td>
      </tr>
    </table>

    <div>选择数量：{{isActiveFruit}}/{{totalNum}}</div>
    <div>总价: {{totalPrice}}</div>
  </div>
</template>

<script>
export default {
  props: ['shopListItem'],
  methods: {
    // 单项数据流，不推荐在子组件内修改数组
    // 子组件需要修改父组件的数据时，只需告诉父组件
    add (index) {
      this.shopListItem[index].num += 1
    },
    reduce (index) {
      let number = this.shopListItem[index].num
      if (number > 1) {
        this.shopListItem[index].num -= 1
      } else {
        if (window.confirm('您确定要删除吗？')) {
          this.$emit('removeItem', index)
        }
      }
    }
  },
  computed: {
    isActiveFruit () {
      return this.shopListItem.filter(item => item.isActive).length
    },
    totalNum () {
      return this.shopListItem.length
    },
    totalPrice () {
      let totalPrice = 0
      this.shopListItem.forEach(ele => {
        if (ele.isActive) {
          totalPrice += ele.num * ele.price
        }
      })
      return totalPrice
    }
  }
}
</script>

<style scoped>

</style>