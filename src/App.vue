<script setup>
import { ref } from 'vue'
const text = ref('這是一段文字')
const todos = ref([
  {
    id: 1,
    text: 'asdgvfgb'
  }
])
const tempEdit = ref({
  id: '',
  text: ''
})
const addTodo = () => {
  todos.value.push({
    text: text.value,
    id: new Date().getTime()
  })
  console.log(todos.value)
  text.value = ''
}
const deleteTodo = (todo) => {
  console.log(todo)
  const index = todos.value.findIndex((item) => item.id === todo.id)
  todos.value.splice(index, 1)
}
const prepareEdit = (todo) => {
  tempEdit.value = { ...todo }
  console.log(tempEdit.value)
}
const confirmEdit = () => {
  const index = todos.value.findIndex((item) => item.id === tempEdit.value.id)
  todos.value[index] = tempEdit.value
  tempEdit.value = {}
}
</script>

<template>
  <input type="text" v-model="text" />
  <button type="button" @click="addTodo">新增</button>
  <div class="todo" v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
    <button type="button" @click="deleteTodo(todo)">刪除</button>
    <button type="button" @click="prepareEdit(todo)">編輯</button>
    <hr />
  </div>
  <hr />
  <div v-if="tempEdit.id">
    <h3>編輯區域</h3>
    目前修改的值：{{ tempEdit.text }} <br />
    <input type="text" v-model="tempEdit.text" />
    <button type="button" @click="confirmEdit(todo)">確認編輯</button>
    <button type="button" @click="tempEdit = {}">取消編輯</button>
  </div>
</template>

<style scoped>
button {
  font-weight: bold;
}
.todo {
  display: block;
  padding: 10px 0;
}
</style>
