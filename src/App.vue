<script setup>
import { ref } from 'vue'

const drinks = ref([
  {
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])

const incrementStock = (index) => {
  drinks.value[index].stock++
}

const decrementStock = (index) => {
  if (drinks.value[index].stock > 0) {
    drinks.value[index].stock--
  }
}

const currentDrink = ref(null)
const editDrink = (index) => {
  currentDrink.value = { ...drinks.value[index], index }
}

const saveDrink = () => {
  const { index, ...updatedDrink } = currentDrink.value
  drinks.value[index] = updatedDrink
  currentDrink.value = null
}

const cancelEdit = () => {
  currentDrink.value = null
}
</script>

<template>
  <div>
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody v-for="(item, index) in drinks" :key="index">
        <tr>
          <td>{{ item.name }}</td>
          <td>
            <small>{{ item.description }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <button @click="decrementStock(index)">-</button>
            {{ item.stock }}
            <button @click="incrementStock(index)">+</button>
          </td>
          <td>
            <button type="button" @click="editDrink(index)">修改</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="currentDrink">
      <h3>修改品項</h3>
      <form @submit.prevent="saveDrink">
        <div>
          <label for="name">名稱:</label>
          <input id="name" v-model="currentDrink.name" />
        </div>
        <div>
          <label for="description">描述:</label>
          <input id="description" v-model="currentDrink.description" />
        </div>
        <div>
          <label for="price">價格:</label>
          <input id="price" type="number" v-model="currentDrink.price" />
        </div>
        <div>
          <label for="stock">庫存:</label>
          <input id="stock" type="number" v-model="currentDrink.stock" />
        </div>
        <button type="submit">保存</button>
        <button type="button" @click="cancelEdit">取消</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
table {
  border-collapse: collapse;
}

th,
td {
  padding: 15px;
  text-align: center;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
}

td button {
  margin: 0 5px;
}
</style>
