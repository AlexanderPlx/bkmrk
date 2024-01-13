<script setup lang="ts">
import { useWinBox } from 'vue-winbox'
import { MenuOption } from 'naive-ui'

type MainMenuOption = MenuOption & { url?: string }

const createWinBox = useWinBox()

const openRecord = (url?: string) => {
  const randomId = Math.floor(Math.random() * 20) + 1

  createWinBox({
    title: url ?? `Fox #${randomId}`,
    url: url ?? `https://randomfox.ca/images/${randomId}.jpg`,
    class: 'modern',
  })
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

const handleUpdateValue = (key: string, item: MainMenuOption) => {
  const url = item.url

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
