<template>
  <div style="display: inline-block">
    <!-- 后退 -->
    <Tooltip :content="$t('history.revocation') + `(${undoStack.length})`">
      <Button @click="undo" type="text" size="small" :disabled="undoStack.length === 0">
        <Icon type="ios-undo" size="20" />
      </Button>
    </Tooltip>

    <!-- 恢复 -->
    <Tooltip :content="$t('history.redo') + `(${redoStack.length})`">
      <Button @click="redo" type="text" size="small" :disabled="redoStack.length === 0">
        <Icon type="ios-redo" size="20" />
      </Button>
    </Tooltip>
  </div>
</template>

<script setup lang="ts">
import useSelect from '@/hooks/select';
const { canvasEditor } = useSelect();
const { redoStack, undoStack } = reactive(canvasEditor.getHistory());

// 后退
const undo = () => {
  canvasEditor.undo();
};
// 恢复
const redo = () => {
  canvasEditor.redo();
};
</script>

<style scoped lang="less">
span.active {
  svg.icon {
    fill: #2d8cf0;
  }
}
</style>

<script lang="ts">
export default {
  name: 'ToolBar',
};
</script>
