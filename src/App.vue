<script setup lang="ts">
import { darkTheme } from 'naive-ui'
import { ref } from 'vue'

import MainMenu from './components/MainMenu.vue'
import ToolBar from './components/ToolBar.vue';

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
            content-style="padding: 12px;
                            display: flex;
                            flex-direction: column;
                            justify-content: space-between;"
        >
          <n-message-provider :placement="'bottom-left'">
            <MainMenu />
          </n-message-provider>

          <ToolBar class="button-group"
                   v-bind:theme="theme"
                   @changeTheme="(value) => theme = value"
          />
        </n-layout-sider>
        <n-layout>
        </n-layout>
      </n-layout>
    </n-space>
  </n-config-provider>
</template>

<style scoped>
  .button-group {
    align-self: center;
  }
</style>
