<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @change="checkChange"/>
      <span>{{ todo.todoName }}</span>
    </label>
    <button class="btn btn-danger" @click="deleteItemId()">删除</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  props: ['todo'],
  methods: {
    deleteItemId() {
      this.$bus.$emit('deleteItem',this.todo.id)
    },
    checkChange() {
      this.$bus.$emit('checkChange',this.todo.id)
    }
  }
}
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:hover button {
  display: block;
}

li:hover {
  background: #f5f5f5;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
</style>