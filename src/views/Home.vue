<template>
  <div id="app">
    <h1>我的购物车</h1>

    <div>
      <h2>添加水果</h2>
      <div>
        <label for="">水果名称</label>
        <input type="text" placeholder="请输入水果名称" v-model="fruitInfo.name">
      </div>
      <div>
        <label for="">水果价格</label>
        <input type="text" placeholder="请输入水果价格" v-model="fruitInfo.price">
      </div>
      <div>
        <button @click="addToList">添加水果</button>
      </div>
    </div>

    <div>
      <h2>水果列表</h2>
      <table>
        <tr>
          <th>水果名称</th>
          <th>水果价格</th>
          <th>操作</th>
        </tr>
        <tr v-for="(item,index) in fruitList" :key="item.id">
          <td>{{item.name}}</td>
          <td>{{item.price}}</td>
          <td><button  @click="addToShopCar(index)">添加到购物车</button></td>
        </tr>
      </table>
    </div>

    <cart :shopListItem="shopListItem" @removeItem="remove"></cart>
  </div>
</template>

<script>
// @ is an alias to /src
import Cart from '@/components/cart.vue'

export default {
  name: 'home',
  data(){
    return {
      title: "我的购物车",
      shopListItem: [], // 购物车数据
      fruitList: [
        {
          id:0,
          name: '红富士苹果',
          price: 50,
          unit: '斤'
        },
         {
           id:1,
          name: '香蕉',
          price: 100,
          unit: '斤'
        },
         {
           id:2,
          name: '西瓜',
          price: 11,
          unit: '斤'
        },
      ],
      fruitInfo: {
        name: null,
        price: null
      }
    }
  },
  components: {
    Cart
  },
  methods: {
    addToList () {
      this.fruitList.push(this.fruitInfo)
    },
    addToShopCar (index) {
      let item = this.fruitList[index]
      // 判断购物车是否存在 已有的水果
      let isHasItem = this.shopListItem.find( (x) => x.id === item.id)
      if(isHasItem){
        isHasItem.num += 1
      } else {
        this.shopListItem.push({
          ...item,
          num: 1,
          isActive: true
        })
      }
      
    },
    // 删除操作
    remove (index) {
      this.shopListItem.splice(index, 1)
    }
  }
}
</script>
