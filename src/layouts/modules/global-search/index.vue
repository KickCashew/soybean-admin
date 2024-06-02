<script lang="ts" setup>
import { useBoolean } from '@sa/hooks';
import { onKeyStroke } from '@vueuse/core';
import { $t } from '@/locales';
import { useAppStore } from '@/store/modules/app';
import SearchModal from './components/search-modal.vue';

defineOptions({ name: 'GlobalSearch' });

const { bool: show, toggle } = useBoolean();

const appStore = useAppStore();

onKeyStroke(
  ['Control', 'k'],
  e => {
    e.preventDefault();
    if (e.ctrlKey && e.key === 'k' && !show.value) {
      appStore.closeThemeDrawer();
      toggle();
    }
  },
  { dedupe: true }
);
</script>

<template>
  <ButtonIcon :tooltip-content="$t('common.search')" @click="toggle">
    <icon-uil-search />
  </ButtonIcon>
  <SearchModal v-model:show="show" />
</template>

<style lang="scss" scoped></style>
