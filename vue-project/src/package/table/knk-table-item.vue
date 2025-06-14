<script setup>

const props = defineProps({
  slots: Object,
  row: Object,
  columns: Array
})

</script>

<template>
  <tr>
    <td v-for="col in columns">
      <template
          v-if="slots[col.slotKey] && col.slotKey"
          v-for="(_, name) in slots[col.slotKey]">
        <component :is="() => slots[col.slotKey][name]({row: row})"/>
      </template>
      <template v-else>{{row[col.prop]}}</template>
    </td>
  </tr>
</template>

<style scoped>

</style>