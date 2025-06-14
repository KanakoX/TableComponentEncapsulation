<script setup>

import {onBeforeUnmount, ref, watch} from "vue";

const props = defineProps({
  visible: {
    type: Boolean,
    required: true,
    default: false
  },
  handleClose: {
    type: Function,
    required: true
  }
})

// 用于控制display: none
const display = ref(props.visible)
// 用于控制class: is-show
const visible = ref(props.visible)
// 计时器
let timer = 0

watch(() => props.visible, (curV) => {
  console.log(curV)
  clearTimeout(timer)
  // 开启弹窗
  if (curV) {
    display.value = true
    timer = setTimeout(() => {
      visible.value = true
      clearTimeout(timer)
    }, 20)
  }
  // 关闭弹窗
  else {
    visible.value = false
    timer = setTimeout(() => {
      display.value = false
      clearTimeout(timer)
    }, 500)
  }
})

onBeforeUnmount(() => {
  clearTimeout(timer)
})

</script>

<template>
  <div class="dialog-container"
       :class="{'is-show': visible}"
       :style="display ? '' : 'display: none;'">
<!--    遮罩-->
    <div class="dialog-cover" @click="props.handleClose"/>

<!--    对话框主体-->
    <div class="dialog-main">
<!--      <button class="btn-close">x</button>-->
      <!--    内容-->
      <div class="dialog-body">
        <slot></slot>
      </div>
    </div>

  </div>
</template>

<style scoped>
.dialog-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 999;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: .5s;
  visibility: hidden;
  opacity: 0;

  &.is-show {
    visibility: visible;
    opacity: 1;
    .dialog-main {
      transform: translateY(0);
    }
  }
}

.dialog-cover {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  background-color: rgba(0, 0, 0, .1);
}

.dialog-main {
  position: relative;
  background: #f6f6f6;
  min-width: 340px;
  min-height: 100px;
  border-radius: 10px;
  box-shadow: 2px 2px 30px 2px rgba(0, 0, 0, .1);
  border: 1px solid rgba(0, 0, 0, .1);
  padding: 8px;
  transition: .5s;
  transform: translateY(100%);
}

@media screen and (max-width: 600px) {
  .dialog-container {
    flex-direction: column;
    justify-content: flex-end;
    .dialog-main {
      min-width: unset;
      width: 100%;
      border-radius: 20px 20px 0 0;
    }
  }
}

</style>