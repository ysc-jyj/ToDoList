<template>
    <!-- 待办分类 -->
    <div class="filters">
      <!-- change-filter将变化传给父组件 -->
        <span class="filter" v-for="filter in filters" :key = 'filter.val' @click="$emit('change-filter',filter.val)" :class="filter.val === active ? 'active':''">{{filter.label}}</span>
    </div>
</template>

<script>
export default {
  name: 'ToDoFilter',
  data () {
    return {
      filters: [
        { label: 'all', val: 'all' },
        { label: 'done', val: 'done' },
        { label: 'todo', val: 'todo' }
      ]
    }
  },
  // 接收父组件的信息
  props: ['active']
}
</script>

<style lang="less">
    .filters{
      font-size:16px;
      .filter{
        color:#ccc;
        display: inline-block;
        margin: 10px 10px 10px 0;
        &.active{
          color: rgb(162, 195, 238);
          font-size: 18px;
          font-weight: 600;
        }
        &:hover{
          cursor:pointer;
        }
      }
    }
</style>
