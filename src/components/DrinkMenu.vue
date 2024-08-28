<script setup>
  import { ref } from 'vue';

  const drinkList = ref([
    {
      name: '珍珠奶茶',
      describe: '香濃奶茶搭配QQ珍珠',
      price: 50,
      stock: 20
    },
    {
      name: '冬瓜檸檬',
      describe: '清新冬瓜配上新鮮檸檬',
      price: 45,
      stock: 18
    },
    {
      name: '翡翠檸檬',
      describe: '綠茶與檸檬的完美結合',
      price: 55,
      stock: 34
    },
    {
      name: '四季春茶',
      describe: '香醇四季春茶，回甘無比',
      price: 45,
      stock: 10
    },
    {
      name: '阿薩姆奶茶',
      describe: '阿薩姆紅茶搭配香醇鮮奶',
      price: 50,
      stock: 25
    },
    {
      name: '檸檬冰茶',
      describe: '檸檬與冰茶的清新組合',
      price: 45,
      stock: 20
    },
    {
      name: '芒果綠茶',
      describe: '芒果與綠茶的獨特風味',
      price: 55,
      stock: 18
    },
    {
      name: '抹茶拿鐵',
      describe: '抹茶與鮮奶的絕配',
      price: 60,
      stock: 20
    },
  ])
  const tempName = ref('')
  const editTarget = ref('')
  const reduce = (item) => {
    if(item.stock > 0){
      item.stock--
    }
  }
  const add = (item) => item.stock++
  const editName = (item, index) => {
    let edit = {...item};
    let newInedx = index + 1;
    tempName.value = edit.name;
    editTarget.value = newInedx;
  }
  const cancel = () => {
    editTarget.value = ''
    tempName.value = ''
  }
  const complete = (item) => {
    item.name = tempName.value;
    tempName.value = '';
    cancel();
  }
</script>

<template>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in drinkList" :key="index">
        <td>
          <div v-if="editTarget && (index+1) == editTarget">
            <input type="text" v-model="tempName">
            <button type="button" class="cancel" @click="cancel">取消</button>
            <button type="button" class="complete" @click="complete(item)">完成</button>
          </div>
          <div v-else>
            {{ item.name }}
            <button type="button" class="edit" @click="editName(item, index)" v-if="!editTarget || (index+1) !== editTarget">編輯</button>
          </div>
        </td>
        <td>{{ item.describe }}</td>
        <td>{{ item.price }}</td>
        <td class="stock">
          <button type="button" class="reduce" @click="reduce(item)">-</button>
          {{ item.stock }}
          <button type="button" class="add" @click="add(item)">+</button></td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
  table {
    width: 80vw;
    border-collapse: collapse;
  }
  thead {
    border-style: solid;
    border-color: #d6d6d6;
    border-width: 1px 0px 3px 0px;
  }
  thead tr th:nth-child(1) {
    width: 30%;
  }
  thead tr th:nth-child(2) {
    width: 40%;
  }
  thead tr th:nth-child(3) {
    width: 15%;
  }
  thead tr th:nth-child(4) {
    width: 15%;
  }
  th {
    font-weight: bold;
    text-align: left;
    padding: 8px;
  }
  tbody tr:nth-of-type(2n+1) {
    background-color: rgb(0, 0, 0, 0.05);
  }
  tbody td {
    padding: 8px;
    margin: 0;
  }
  input {
    margin-right: 4px;
  }
  button {
    margin: 0 4px;
  }
  .edit {
    background-color: #0d6efd;
    color: #fff;
    border-radius: 5px;
    border: 1px solid #0d6efd;
  }
  .cancel {
    background-color: #dc3545;
    color: #fff;
    border-radius: 5px;
    border: 1px solid #dc3545;
  }
  .complete {
    background-color: #198754;
    color: #fff;
    border-radius: 5px;
    border: 1px solid #198754;
  }
  .stock {
    display: flex;
    align-items: center;
  }
  .reduce, .add {
    width: 1.6rem;
    height: 1.6rem;
    background-color: #fff;
    border: 1px solid #d6d6d6;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>