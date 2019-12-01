<template>
  <div class="wrap">
    <ul class="list-wrap">
      <li class="item-name-wrap" v-for="item in arrayList" :key="item.id">
        <div :class="{'active': selectedId == item.id}" @click="bindClickActive(item.id)">
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
      <todo :selectedTodo="selectedTodo"></todo>
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
      arrayList: [],
      selectedId: '',
      selectedTodo: [
        {
          "id": "1",
          "name": "Jack",
          "active": true,
          "todo": [
            {
              "id": "1list1",
              "text": "早点睡吧",
              "status": true
            }
          ]
        }
      ]
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
          othis.selectedId = res.data[0].id
          othis.setSelectedTodoArray()
          console.log(othis.selectedTodo)
      })
    },
    addItem: function () {
      var othis = this
      var list = othis.arrayList
      var len = othis.arrayList.length
      var newItem = new Object()
      newItem.id = (len + 1)
      newItem.name = "newName"
      newItem.active = false
      newItem.todo = []
      this.selectedId = newItem.id
      othis.arrayList.push(newItem)
      othis.setSelectedTodoArray()
    },
    bindClickActive: function (id) {
      this.selectedId = id
      this.setSelectedTodoArray()
      console.log(this.selectedTodo)
    },
    setSelectedTodoArray: function () {
      this.selectedTodo = []
      this.selectedTodo.push(this.arrayList.find((t, index) => {
        return this.selectedId && t.id == this.selectedId
      }))
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
      div
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
      .active
        opacity 1
    .item-add
      color #5db9ff
  .todo-wrap
  	flex 1 0 auto
</style>
