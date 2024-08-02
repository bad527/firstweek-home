<script setup>
import { ref } from 'vue'
const tasks = ref([
  {
    item: '珍珠奶茶',
    describe: '<small>香濃奶茶搭配QQ珍珠</small>',
    price: 50,
    Inventory: 20
  },
  {
    item: '冬瓜檸檬',
    describe: '<small>清新冬瓜配上新鮮檸檬</small>',
    price: 45,
    Inventory: 18
  },
  {
    item: '翡翠檸檬',
    describe: '<small>綠茶與檸檬的完美結合</small>',
    price: 55,
    Inventory: 34
  },
  {
    item: '四季春茶',
    describe: '<small>香醇四季春茶，回甘無比</small>',
    price: 45,
    Inventory: 10
  },
  {
    item: '阿薩姆奶茶',
    describe: '<small>阿薩姆紅茶搭配香醇鮮奶</small>',
    price: 50,
    Inventory: 25
  },
  {
    item: '檸檬冰茶',
    describe: '<small>檸檬與冰茶的清新組合</small>',
    price: 45,
    Inventory: 20
  },
  {
    item: '芒果綠茶',
    describe: '<small>芒果與綠茶的獨特風味</small>',
    price: 55,
    Inventory: 18
  },
  {
    item: '抹茶拿鐵',
    describe: '<small>抹茶與鮮奶的絕配</small>',
    price: 60,
    Inventory: 20
  }
])

const editingIndex = ref(null)
const editingName = ref('')

const starEditing = (index, item) => {
  editingIndex.value = index
  editingName.value = item
}

const saveItem = (task) => {
  task.item = editingName.value
  editingIndex.value = null
}
const cancelEditing = () => {
  editingIndex.value = null
}

const decrementInventory = (task) => {
  task.Inventory--
}
const incrementInventory = (task) => {
  task.Inventory++
}
</script>

<template>
  <div id="app" class="container">
    <div class="table">
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">編輯品項</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <div v-if="editingIndex === index">
              <input v-model.trim="editingName" />
            </div>
            <div v-else>
              {{ task.item }}
            </div>
          </td>
          <td v-html="task.describe"></td>
          <td>{{ task.price }}</td>
          <td>
            <button @click="decrementInventory(task)">-</button>
            {{ task.Inventory }}
            <button @click="incrementInventory(task)">+</button>
          </td>
          <td>
            <div v-if="editingIndex === index">
              <button @click="saveItem(task)" class="btn btn-primary">儲存</button>
              <button @click="cancelEditing" class="btn btn-primary">取消</button>
            </div>
            <div v-else>
              <button @click="starEditing(index, task.item)" class="btn btn-warning">
                編輯品項
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </div>
  </div>
</template>

<style>
.container {
  margin-top: 50px;
}
.table {
  width: 50vw;
  border-collapse: collapse;
}
.table th,
.table td {
  border: 1px solid #ddd;
  padding: 8px;
  width: 12vw;
  text-align: center;
}

td input {
  border: none;
  text-align: center;
}
</style>
