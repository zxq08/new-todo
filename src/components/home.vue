<template>
  <div class="wrap">
    <ul class="list-wrap">
      <li class="item-name-wrap" v-for="item in arrayList" :key="item.id">
        <div :class="item.active ? 'item-name active' :'item-name'" @click="bindClickActive">
          <span class="iconfont">&#xe606;</span>
          <span class="item-text">{{item.name}}</span>
          <span class="item-num">1</span>
        </div>
      </li>
      <li class="item-name-wrap" @click="addItem">
        <div class="item-name item-add">
          <span>+</span>
          <span class="item-text">新增</span>
        </div>
      </li>
    </ul>
    <div class="todo-wrap">
      <todo></todo>
    </div>
  </div>
</template>
<script>
import Todo from './todo'
import axios from 'axios'

export default {
  name: 'Home',
  data: function () {
    return {
      arrayList: []
    }
  },
  components: {
    Todo
  },
  methods: {
    getList: function () {
      var othis = this
      axios.get('./mock/list.json')
        .then(function (res) {
          othis.arrayList = res.data
      })
    },
    addItem: function () {
      var othis = this
      var list = othis.arrayList
      var len = othis.arrayList.length
      var newItem = new Object()
      newItem.id = '0' + (len + 1)
      newItem.name = "newName"
      newItem.active = false
      newItem.todo = []
      othis.arrayList.push(newItem)
    },
    bindClickActive: function () {
      var othis = this
      console.log(othis.key)
    }
  },
  created () {
    this.getList()
  }
}
</script>
<style lang="stylus" scoped>
.wrap
  width 80vw
  margin 0 auto
  display flex
  .list-wrap
    width 24%
    .item-name-wrap
      border-bottom .5px solid rgba(238, 238, 238, .4)
      .item-name
        box-sizing border-box
        width 100%
        height 65px
        display flex
        justify-content space-around
        align-items center
        color #fff
        padding 0 10px
        cursor pointer
        opacity 0.5
        &:hover
          opacity 1
        .item-text
          text-align left
          padding-left 10px
          flex 1 0 auto
        .item-num
          width 20px
          height 20px
          border-radius 50%
          background #2cc5d2
          text-align center
          line-height 20px
    .item-add
      color #5db9ff
  .item-name.active
    opacity 1
  .todo-wrap
  	flex 1 0 auto
</style>
