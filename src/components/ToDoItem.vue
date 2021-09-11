<template>
  <!-- 将内容都在进label方便调节自定义的check-button -->
  <div class="todo-item" :class="todo.isComplete?'done':''">
    <label><input type="checkbox" :checked="todo.isComplete" @click="$emit('change-state',$event)">{{todo.todoContent}}<span class="check-button"></span></label>
  </div>
</template>

<script>
export default {
  name: 'ToDoItem',
  // FIXME 加载自动更新
  // 接收父组件的todo
  props: ['todo']
}
</script>

<style lang="less">
.todo-item{
        width: 100%;
        height: 50px;
        line-height: 50px;
        background-color: #fff;
        margin-bottom: 15px;
        padding: 0 15px;
        border-radius: 15px;
        label{
          display: flex;
          align-items: center;
          position: relative;
            .check-button{
              position: absolute;
              &::after,&::before{
                content:" ";
                display: block;
                position: absolute;
                width: 16px;
                height: 16px;
                border-radius: 50%;
              }
              &::before{
                border:2px solid rgb(193, 214, 241);
                transform: translateY(-50%);
              }
              &::after{
                background: rgb(193, 214, 241);
                transform: translate(2px,-50%) scale(0.8);
                opacity: 0;
              }
          }
          input{
            margin-right: 16px;
            opacity: 0;
          }
          input:checked+span.check-button::after{
            opacity: 1;
          }
        }
      }
.done {
  label{
    font-style: italic;
    text-decoration: line-through;
    color:#ccc;
  }
}
</style>
