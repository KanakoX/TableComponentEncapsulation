<script setup>
import KnkTable from "@/package/table/knk-table.vue";
import KnkTableColumn from "@/package/table/knk-table-column.vue";
import {ref} from "vue";

const tableData = ref([
  {id: 1, name: 'Kanako', age: 23, gender: 'male'},
  {id: 2, name: 'Cartethyia', age: 18, gender: 'female'},
  {id: 4, name: 'Tom', age: 4, gender: 'male'},
  {id: 6, name: 'Jerry', age: 3, gender: 'female'},
  {id: 7, name: 'Peter', age: 33, gender: 'male'}
])

</script>

<template>
  <div class="container">
    <knk-table :data="tableData">
      <knk-table-column prop="id" label="id"/>
      <knk-table-column prop="name" label="姓名" width="100px"/>
      <knk-table-column prop="age" label="年龄"/>
      <knk-table-column prop="gender" label="性别" width="80px"/>
      <knk-table-column label="操作">
        <template #default="scope">
        </template>
      </knk-table-column>
    </knk-table>
  </div>
</template>

<style>
.container {
  width: 100vh;
  height: 100vh;
  background: #4DD0E1;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
