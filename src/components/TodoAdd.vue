<template>
  <div class="input-add">
    <!-- 输入框 -->
    <input type="text" name="todo" v-model="todoContent" @keyup.enter="add" />
    <button @click="add">
      <!--添加按钮 -->
      <i class="plus"></i>
    </button>
  </div>
</template>

<script>
// 组件抽离再导出
export default {
  name: 'ToDoAdd',
  props: ['tid'],
  data () {
    return {
      todoContent: ''
    }
  },
  methods: {
    add () {
      // 得到输入的数据
      this.todoContent = this.todoContent.trim()
      // 检查合法性
      if (!this.todoContent) {
        // FIXME 弹窗
        return
      }
      const todo = {
        id: this.tid,
        isComplete: false,
        todoContent: this.todoContent
      }
      this.$emit('addTodo', todo)
      // 清空输入框
      this.todoContent = ''
    }
  }
}
</script>

<style lang="less">
.input-add {
  display: flex;
  position: relative;
  input {
    padding: 14px 50px 14px 16px;
    width: 100%;
    border-radius: 30px;
    border: none;
    outline: none;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    font-size: 16px;
  }
  button {
    width: 44px;
    height: 44px;
    position: absolute;
    top: 1px;
    right: 2px;
    //横线、竖线
    background: linear-gradient(rgb(182, 200, 250), rgb(217, 217, 247));
    border-radius: 50%;
    border: none;
    outline: none;
    color: #fff;
    .plus {
      display: block;
      width: 100%;
      height: 100%;
      background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
      background-size: 50% 4px, 4px 50%;
      background-position: center;
      background-repeat: no-repeat;
    }
    &:hover {
      cursor: pointer;
    }
  }
}
</style>
