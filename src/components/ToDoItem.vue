<template>
  <!-- 将内容都在进label方便调节自定义的check-button -->
  <div class="todo-item" :class="todo.isComplete ? 'done' : ''">
    <label>
      <input type="checkbox" :checked="todo.isComplete" @click="$emit('change-state', $event)" />
      {{ todo.todoContent}}
      <span class="check-button"></span>
      <button @click="del">
        <!--删除按钮 -->
        <i class="del"></i>
      </button>
    </label>
  </div>
</template>

<script>
export default {
  name: 'ToDoItem',
  // FIXME 加载自动更新
  // 接收父组件的todo
  props: ['todo'],
  methods: {
    del () {
      this.$emit('del-todo', this.todo.id)
    }
  }
}
</script>

<style lang="less">
.todo-item {
  width: 100%;
  height: 50px;
  line-height: 50px;
  background-color: #fff;
  margin-bottom: 15px;
  padding: 0 15px;
  border-radius: 15px;
  label {
    display: flex;
    align-items: center;
    position: relative;
    .check-button {
      position: absolute;
      &::after,
      &::before {
        content: ' ';
        display: block;
        position: absolute;
        width: 16px;
        height: 16px;
        border-radius: 50%;
      }
      &::before {
        border: 2px solid rgb(193, 214, 241);
        transform: translateY(-50%);
      }
      &::after {
        background: rgb(193, 214, 241);
        transform: translate(2px, -50%) scale(0.8);
        opacity: 0;
      }
    }
    input {
      margin-right: 16px;
      opacity: 0;
    }
    input:checked + span.check-button::after {
      opacity: 1;
    }
    button {
      width: 25px;
      height: 25px;
      position: absolute;
      top: 1px;
      right: 2px;
      //横线、竖线
      background: #ddd;
      border-radius: 50%;
      border: none;
      outline: none;
      color: #fff;
      transform: translateY(50%);
      .del {
        display: block;
        width: 100%;
        height: 100%;
        background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
        background-size: 50% 2px, 2px 50%;
        background-position: center;
        background-repeat: no-repeat;
        transform: rotate(45deg);
      }
      &:hover {
        cursor: pointer;
      }
    }
  }
}
.done {
  label {
    font-style: italic;
    text-decoration: line-through;
    color: #ccc;
  }
}
</style>
