<script setup lang="ts">
import { darkTheme } from 'naive-ui'
import MainMenu from './components/MainMenu.vue'
</script>

<template>
  <n-config-provider :theme="darkTheme">
    <n-space vertical size="large">
      <n-layout has-sider bordered style="height: 100vh">
        <n-layout-sider
            bordered
            show-trigger
            :show-collapsed-content="false"
            content-style="padding: 12px;"
        >
          <n-message-provider :placement="'bottom-left'">
            <MainMenu />
          </n-message-provider>
        </n-layout-sider>
        <n-layout>
        </n-layout>
      </n-layout>
    </n-space>
  </n-config-provider>
</template>

<style scoped>

</style>
