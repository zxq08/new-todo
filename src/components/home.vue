<template>
  <div class="wrap">
    <ul class="list-wrap">
      <li v-for="item in arrayList" :key="item.id">
        <div class="item-name">
          <span>@</span>
          <span class="item-text">{{item.name}}</span>
          <span class="item-num">1</span>
        </div>
      </li>
      <li class="item-add item-name">
        <span>+</span>
        <span class="item-text">新增</span>
      </li>
    </ul>
    <div class="todo-wrap">
      <todo></todo>
    </div>
  </div>
</template>
<script>
import Todo from './todo'

export default {
  name: 'Home',
  data: function () {
    return {
      arrayList: [
        {
          id: '01',
          name: 'Jack',
          todo: []
        }, {
          id: '02',
          name: 'Mary',
          todo: []
        }, {
          id: '03',
          name: 'Ming',
          todo: []
        }
      ]
    }
  },
  components: {
    Todo
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
    .item-name
      box-sizing border-box
      width 100%
      height 65px
      border-bottom 1px solid #eee
      display flex
      justify-content space-around
      align-items center
      color #fff
      padding 0 10px
      cursor pointer
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
  .todo-wrap
  	flex 1 0 auto
</style>
