<script setup lang="ts">
import { darkTheme } from 'naive-ui'
import MainMenu from './components/MainMenu.vue'
import { ref } from 'vue'

const theme = ref(darkTheme);
const showModalSettings = ref(false);

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

          <n-button-group class="button-group">
            <n-button round>
              Login
            </n-button>
            <n-button round
                      @click="showModalSettings = true"
            >
              Settings
              <template>
                <n-modal v-model:show="showModalSettings">
                  <n-card
                      style="width: 600px"
                      title="Settings"
                      :bordered="true"
                      size="huge"
                      role="dialog"
                      aria-modal="true"
                  >
                    <n-switch
                        :default-value="!theme"
                        @update:value="(v) => v ? theme = null : theme = darkTheme"
                    >
                      <template #checked>
                        Light theme
                      </template>
                      <template #unchecked>
                        Dark theme
                      </template>
                    </n-switch>
                  </n-card>
                </n-modal>
              </template>
            </n-button>
          </n-button-group>
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
