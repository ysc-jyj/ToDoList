<template>
  <!-- TODO 删除 -->
  <div id="app">
    <div class="container">
      <h1>ToDo List</h1>
      <ToDoAdd @addTodo="handleAdd" :tid="todos.length+1"></ToDoAdd>
      <!-- 通过active动态绑定activeFilter传递 接收子组件的选中分类 -->
      <ToDoFilter :active="activeFilter" @change-filter="activeFilter = $event"></ToDoFilter>
      <ToDoList :todos="filterTodos" @del-todo="delTodo"></ToDoList>
    </div>
    <!--  <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />-->
  </div>
</template>
<script>
// 组件导入
import ToDoAdd from './components/TodoAdd.vue'
import ToDoFilter from './components/ToDoFilter.vue'
import ToDoList from './components/ToDoList.vue'
export default {
  name: 'App',
  components: {
    ToDoAdd,
    ToDoFilter,
    ToDoList
  },
  data () {
    return {
      todos: [],
      // 判断当前的选中的
      activeFilter: 'all'
    }
  },
  methods: {
    handleAdd (todo) {
      this.todos.unshift(todo)
      console.log(this.todos)
    },
    delTodo (id) {
      this.todos = this.todos.filter((val) => {
        if (val.id !== id) {
          return val
        }
      })
    }
  },
  computed: {
    // 返回分类后的todoList
    filterTodos () {
      let filtersTodos = this.todos
      // 通过选中的过滤出需要的数组
      if (this.activeFilter === 'done') {
        filtersTodos = this.todos.filter((v) => {
          return v.isComplete
        })
      } else if (this.activeFilter === 'todo') {
        filtersTodos = this.todos.filter((v) => {
          return !v.isComplete
        })
      }
      return filtersTodos
    }
  }
}
</script>

<style lang="less">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* 整个页面 */
#app {
  width: 100vw; //浏览器宽度
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(193, 214, 241);
}
.container {
  width: 60%;
  max-width: 400px;
  border-radius: 15px;
  padding: 40px 25px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  background-color: rgb(245, 246, 252);
  h1 {
    color: #374450;
    font-size: 30px;
    text-align: center;
    margin-bottom: 20px;
  }
}
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #42b983;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
