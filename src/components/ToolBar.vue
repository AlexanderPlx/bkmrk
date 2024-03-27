<script setup lang="ts">

import { darkTheme } from 'naive-ui';
import { ref } from 'vue';

const props = defineProps(['theme']);
const emit = defineEmits(['changeTheme']);

const showModalSettings = ref(false);
const showModalLogin = ref(false);

let login = ref();
let password = ref();

function onChangeTheme(value: boolean) {
  value ? emit('changeTheme', null) : emit('changeTheme', darkTheme);
}

</script>

<template>
  <n-button-group>
    <n-button round
              @click="showModalLogin = true"
    >
      Login
      <template>
        <n-modal v-model:show="showModalLogin">
          <n-card
              style="width: 600px"
              title="LogIn/LogOut"
              :bordered="true"
              size="huge"
              role="dialog"
              aria-modal="true"
          >
            <form>
              <n-input
                  type="text"
                  placeholder="Login"
                  :maxlength="12"
                  style="margin-bottom: 10px"
                  v-model:value.lazy.trim="login"
              />
              <n-input
                  type="password"
                  show-password-on="mousedown"
                  placeholder="Password"
                  :maxlength="8"
                  style="margin-bottom: 10px"
                  v-model:value.lazy.trim="password"
              />
            </form>
            <n-button-group>
              <n-button round
                        @click="console.log('Login', login, 'password', password)">
                Login
              </n-button>
              <n-button round
                        @click="console.log('Register')">
                Register
              </n-button>
            </n-button-group>
          </n-card>
        </n-modal>
      </template>
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
                :default-value="!props.theme"
                @update:value="onChangeTheme"
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
</template>

<style scoped>

</style>