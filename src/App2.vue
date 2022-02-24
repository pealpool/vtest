<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :getAddItem="getAddItem"/>
        <MyList :todos="todos"/>
        <MyFooter :todos="todos"/>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from "@/components/MyHeader";
import MyFooter from "@/components/MyFooter";
import MyList from "@/components/MyList";

export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: '001', todoName: '抽烟', done: true},
        {id: '002', todoName: '喝酒', done: false},
        {id: '003', todoName: '烫头', done: true}
      ]
    }
  },
  components: {MyHeader, MyFooter, MyList},
  methods: {
    getAddItem(addObj) {
      this.todos.unshift(addObj)
    },
    deleteItem(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    doneChange(id) {
      this.todos.forEach(function (e) {
        if (e.id === id) {
          e.done = !e.done
        }
      })
    },
    selectAllBtn(tf) {
      if (tf) {
        this.todos.forEach(e => {
          e.done = true
        })
      } else {
        this.todos.forEach(e => {
          e.done = false
        })
      }
    }
  },
  mounted() {
    this.$bus.$on('checkChange', this.doneChange)
    this.$bus.$on('deleteItem', this.deleteItem)
    this.$bus.$on('selectAllBtn', this.selectAllBtn)
  },
  beforeDestroy() {
    this.$bus.$off('checkChange')
    this.$bus.$off('deleteItem')
    this.$bus.$off('selectAllBtn')
  }
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
