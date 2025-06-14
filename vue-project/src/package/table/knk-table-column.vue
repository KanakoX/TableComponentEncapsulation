<script setup>
import {inject, onMounted, useSlots} from "vue";

const props = defineProps({
  prop: String,
  label: String,
  width: [String, Number]
})

// 获取插槽
const slots = useSlots()
const slotKey = Symbol('table-slot')

onMounted(() => {
  const regHeaders = inject('regHeaders')
  regHeaders({
    prop: props.prop,
    label: props.label,
    width: props.width,
    slotKey: slotKey
  }, slots)
})

</script>