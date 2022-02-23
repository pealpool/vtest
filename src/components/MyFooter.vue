<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="allCheckBox" @change="selectAllBtn"/>
    </label>
    <span>已完成{{ doneNum }}</span>
    <span>/ 全部{{ allNum }}</span>
    <button class="btn btn-danger">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  data() {
    return {
      allCheckBox: false
    }
  },
  props: ['todos'],
  computed: {
    allNum() {
      return this.todos.length
    },
    doneNum() {
      let i = 0
      this.todos.forEach(function (e) {
        if (e.done === true) i++
      })
      return i
    }
  },
  methods: {
    selectAllBtn() {
      this.$bus.$emit('selectAllBtn', this.allCheckBox)
    }
  },
  watch: {
    todos: {
      immediate: true,
      deep: true,
      handler() {
        let i = 0
        this.todos.forEach(e => {
          if (e.done === true) i++
        })
        if (i === this.todos.length) {
          this.allCheckBox = true
        } else {
          this.allCheckBox = false
        }
      }
    }
  }
}
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>