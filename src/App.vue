<script setup lang="ts">
import { darkTheme } from 'naive-ui'
import MainMenu from './components/MainMenu.vue'
import { ref } from 'vue'

const theme = ref(darkTheme);
</script>

<template>
  <n-config-provider :theme="theme">
    <n-space vertical size="large">
      <n-layout has-sider bordered style="height: 100vh">
        <n-layout-sider
            bordered
            show-trigger
            :show-collapsed-content="false"
            content-style="padding: 12px;"
        >
          <n-switch
              @update:value="(v) => v ? theme = null : theme = darkTheme"
          >
            <template #checked>
              Light theme
            </template>
            <template #unchecked>
              Dark theme
            </template>
          </n-switch>
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
