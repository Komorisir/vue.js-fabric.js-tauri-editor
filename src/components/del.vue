<template>
  <Tooltip v-if="mixinState.mSelectMode" :content="$t('quick.del')">
    <Button @click="del" icon="ios-trash" type="text"></Button>
  </Tooltip>
</template>

<script setup name="Del">
import useSelect from '@/hooks/select';
import { debounce } from 'lodash-es';

const { mixinState, canvasEditor } = useSelect();

const del = debounce(function () {
  canvasEditor.del();
}, 300);
</script>
