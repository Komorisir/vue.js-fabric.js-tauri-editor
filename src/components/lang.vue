<template>
  <Dropdown @on-click="setLang">
    <Button type="text">
      {{ lang }}
      <Icon type="ios-arrow-down"></Icon>
    </Button>
    <template #list>
      <DropdownMenu>
        <DropdownItem v-for="lang in langList" :key="lang.langType" :name="lang.langType">
          {{ lang.langName }}
        </DropdownItem>
      </DropdownMenu>
    </template>
  </Dropdown>
</template>

<script setup name="saveBar">
import { setLocal } from '@/utils/local';
import { LANG } from '@/config/constants/app';

import { useI18n } from 'vue-i18n';
const { locale } = useI18n();

const LANGMAP = {
  zh: '简体中文',
  en: 'English',
  tw: '繁体中文',
  pt: 'Português',
  jp: '日本語',
};

let langList = reactive(
  Object.keys(LANGMAP).map((key) => ({ langType: key, langName: LANGMAP[key] }))
);

const lang = computed(() => {
  return LANGMAP[locale.value];
});

// 设置语言
const setLang = (type) => {
  locale.value = type;
  setLocal(LANG, type);
};
</script>

<style scoped lang="less"></style>
