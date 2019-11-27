<template>
  <div class="todo">
    <div class="header-wrap">
    </div>
    <ul class="todo-content">
      <li>1</li>
      <li>2</li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'Todo'
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
</style>
