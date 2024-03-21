<script setup lang="ts">
import { useWinBox } from 'vue-winbox'
import { MenuOption } from 'naive-ui'

type MainMenuOption = MenuOption & { url?: string }

const createWinBox = useWinBox()
const limitOfWinBox = 15;
const winBoxArray = [];
const windowWidth: number = window.innerWidth;
const windowHeight: number = window.innerHeight;
const widthWinBox = 900;
const heightWinBox = 500;

let x = 280;
let y = 0;

const openRecord = (url?: string) => {

  for (let item of winBoxArray) {
    if (item.title === url) {
      item.focus();

      return;
    }
  }

  if (winBoxArray.length === limitOfWinBox) {
    // necessary to add notification of achieved limitOfWinBox
    return
  }

  if ((widthWinBox + x + 15) > windowWidth || (heightWinBox + y + 15) > windowHeight) {
    x = 280;
    y = 0;
  }

  const winBox = createWinBox({
    title: url,
    url: url,
    class: 'modern',
    x: `${x += 20}px`,
    y: `${y += 20}px`,
    width: `${widthWinBox}px`,
    height: `${heightWinBox}px`,
    onclose: () => {
      let index = winBoxArray.findIndex((item) => item.title === winBox.title);
      index !== -1 ? winBoxArray.splice(index, 1) : null;
      return false
    }
  })

  winBoxArray.push(winBox);
}

const menuOptions: MainMenuOption[] & { url?: string } = [
  {
    label: 'Hear the Wind Sing',
    key: 'hear-the-wind-sing',
    url: `https://randomfox.ca/images/1.jpg`
  },
  {
    label: 'Pinball 1973',
    key: 'pinball-1973',
    disabled: true,
    children: [
      {
        label: 'Rat',
        key: 'rat'

      }
    ]
  },
  {
    label: 'A Wild Sheep Chase',
    key: 'a-wild-sheep-chase',
    disabled: true,
  },
  {
    label: 'Dance Dance Dance',
    key: 'Dance Dance Dance',
    children: [
      {
        type: 'group',
        label: 'People',
        key: 'people',
        children: [
          {
            label: 'Narrator',
            key: 'narrator',
          },
          {
            label: 'Sheep Man',
            key: 'sheep-man',
          }
        ]
      },
      {
        label: 'Beverage',
        key: 'beverage',
        children: [
          {
            label: 'Whisky',
            key: 'whisky'

          }
        ]
      },
      {
        label: 'Food',
        key: 'food',
        children: [
          {
            label: 'Sandwich',
            key: 'sandwich'

          }
        ]
      },
      {
        label: 'The past increases. The future recedes.',
        key: 'the-past-increases-the-future-recedes'

      }
    ]
  }
]

const handleUpdateValue = (_key: string, item: MainMenuOption) => {

  const randomId = Math.floor(Math.random() * 20) + 1;
  const url = <string>item.url ?? `https://randomfox.ca/images/${randomId}.jpg`;

  openRecord(url);
}
</script>

<template>
  <n-menu
      @update:value="handleUpdateValue"
      :options="menuOptions"
  />
</template>

<style scoped>
:global(.n-layout-sider--collapsed .n-layout-sider-scroll-container) {
    pointer-events: none;
}
</style>
