<script setup>
import {provide, ref} from "vue";
import KnkTableItem from "@/package/table/knk-table-item.vue";

const props = defineProps({
  data: Array
})

// knk-table-column 列的配置
const headers = ref([])
// 存储插槽
const colSlots = ref({})
// 父组件knk-table向子组件knk-table-column暴露注册列的方法
const regHeaders = (config, slots) => {
  headers.value.push(config)
  if (slots && slots.default) {
    colSlots.value[config.slotKey] = slots
  }
}
provide('regHeaders', regHeaders)

</script>

<template>
  <table style="border: 1px solid black;padding: 2px;text-align: center;min-width: 100px;min-height: 100px">
<!--    表头-->
    <thead>
    <tr>
      <th v-for="col in headers" :style="{'width': col.width}">{{col.label}}</th>
    </tr>
    </thead>
<!--    表体-->
    <tbody>
    <knk-table-item
        v-for="row in data"
        :slots="colSlots"
        :row="row"
        :columns="headers">
    </knk-table-item>
    </tbody>
  </table>
  <div style="display: none"><slot></slot></div>
</template>

<style scoped>
</style>