<template>
  <div class="todo">
    <div class="header-wrap">
      {{selectedTodo[0].name}}
    </div>
    <ul class="todo-content">
      <li v-for="item in todoList" :key="item.id" :class="{'finished': item.status}">
        {{item.text}}
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'Todo',
  data () {
    return {
      todoList: []
    }
  },
  props: {
    selectedTodo: Array
  },
  mounted () {
    console.log(this.selectedTodo)
  },
  watch: {
    selectedTodo () {
      this.todoList = this.selectedTodo[0].todo
    }
  }
}
</script>
<style lang="stylus" scoped>
.todo
  width 100%
  height 95vh
  margin 10px 0
  .header-wrap
    width 100%
    height 70px
    background linear-gradient(180deg,#d0edf5,#e1e5f0)
  .todo-content
    width 100%
    height 90%
    background #fff
    li
      height 40px
      line-height 40px
      padding-left 10px
    .finished
      color #aaa
      text-decoration line-through
</style>
