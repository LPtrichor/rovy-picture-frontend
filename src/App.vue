<template>
  <div id="app">
    <BasicLayout />
  </div>
</template>

<script setup lang="ts">
import BasicLayout from "@/layouts/BasicLayout.vue";
// 测试
import { healthUsingGet } from '@/api/mainController'
import { useLoginUserStore } from '@/stores/useLoginUserStore.ts'

// 尝试获取用户信息
const loginUserStore = useLoginUserStore()
loginUserStore.fetchLoginUser()



healthUsingGet().then((res) => {
  console.log(res)
})

</script>
