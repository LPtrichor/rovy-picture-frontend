<template>
  <div id="globalSider">
    <a-layout-sider
      v-if="loginUserStore.loginUser.id"
      class="sider"
      width="200"
      breakpoint="lg"
      collapsed-width="0"
    >
      <a-menu
        mode="inline"
        v-model:selectedKeys="current"
        :items="menuItems"
        @click="doMenuClick"
      />
    </a-layout-sider>
  </div>
</template>

<script lang="ts" setup>
import { h, ref } from 'vue'
import { PictureOutlined, UserOutlined } from '@ant-design/icons-vue'

import { useRouter } from 'vue-router'
import { useLoginUserStore } from '@/stores/useLoginUserStore.ts'

const loginUserStore = useLoginUserStore()

// 菜单列表
const menuItems = [
  {
    key: '/',
    label: '公共图库',
    icon: () => h(PictureOutlined),
  },
  {
    key: '/my_space',
    label: '我的空间',
    icon: () => h(UserOutlined),
  },
]

const router = useRouter()

// 当前选中菜单
const current = ref<string[]>([])

// 监听路由变化，更新当前选中菜单
router.afterEach((to) => {
  current.value = getSelectedKey(to.path);
  // console.log('Current path:', to.path, 'Selected menu:', current.value); // 调试日志
});

// 根据路径判断选中的菜单项
// 解决高亮丢失问题
function getSelectedKey(path: string): string[] {
  if (path.startsWith('/space')) {
    // 如果以 /space 开头，选中我的空间
    return ['/my_space'];
  }
  // 否则选中实际路径对应的菜单项
  return [path];
}

// 路由跳转事件
const doMenuClick = ({ key }: { key: string }) => {
  router.push({
    path: key,
  })
}
</script>

<style scoped>
.ant-layout-sider {
  background: none;
}
</style>
