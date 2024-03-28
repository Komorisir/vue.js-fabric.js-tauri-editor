<template>
  <div v-if="!mixinState.mSelectMode">
    <Divider orientation="left" plain>{{ $t('color') }}</Divider>
    <Form :label-width="40">
      <FormItem :label="$t('color')" prop="name">
        <ColorPicker v-model="color" @on-change="setThisColor" alpha size="small" transfer />
      </FormItem>
    </Form>
    <Divider orientation="left" plain>{{ $t('color_macthing') }}</Divider>
    <div class="color-list">
      <template v-for="(item, i) in colorList" :key="item.label + i">
        <div class="item">
          {{ item.label }}:
          <span
            v-for="color in item.color"
            :key="color"
            :style="`background:${color}`"
            @click="setColor(color)"
          ></span>
        </div>
      </template>
    </div>
  </div>
</template>

<script setup name="BgBar">
import { ref } from 'vue';
import useSelect from '@/hooks/select';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const { mixinState, canvasEditor } = useSelect();

const colorList = [
  {
    label: t('scenary', { colorSchemeName: '蓝天白云' }),
    color: ['#00BFFF', '#87CEFA', '#ADD8E6', '#B0C4DE', '#B0E0E6', '#AFEEEE', '#E0FFFF'],
  },
  {
    label: t('scenary', { colorSchemeName: '夏日阳光' }),
    color: ['#FFD700', '#FFA500', '#FF6347', '#FF7F50', '#FF8C00', '#FF4500', '#FFA07A'],
  },
  {
    label: t('scenary', { colorSchemeName: '自然森林' }),
    color: ['#228B22', '#008000', '#006400', '#32CD32', '#00FF7F', '#7FFF00', '#9ACD32'],
  },
  {
    label: t('scenary', { colorSchemeName: '温暖秋天' }),
    color: ['#FFA500', '#FF8C00', '#FF7F50', '#FF6347', '#FF4500', '#FF0000', '#8B0000'],
  },
  {
    label: t('scenary', { colorSchemeName: '明亮春天' }),
    color: ['#00FF00', '#7CFC00', '#ADFF2F', '#7FFF00', '#32CD32', '#00FA9A', '#00FF7F'],
  },
  {
    label: t('scenary', { colorSchemeName: '粉色浪漫' }),
    color: ['#FF69B4', '#FF1493', '#C71585', '#DB7093', '#FF00FF', '#FFB6C1', '#FFC0CB'],
  },
  {
    label: t('scenary', { colorSchemeName: '经典黑白' }),
    color: ['#000000', '#808080', '#C0C0C0', '#FFFFFF', '#F5F5F5', '#DCDCDC', '#A9A9A9'],
  },
  {
    label: t('scenary', { colorSchemeName: '海洋深蓝' }),
    color: ['#000080', '#0000CD', '#00008B', '#191970', '#4169E1', '#0000FF', '#1E90FF'],
  },
  {
    label: t('scenary', { colorSchemeName: '魅力紫夜' }),
    color: ['#800080', '#8B008B', '#BA55D3', '#9400D3', '#9932CC', '#DB7093', '#DDA0DD'],
  },
  {
    label: t('scenary', { colorSchemeName: '沙漠之旅' }),
    color: ['#D2B48C', '#D2691E', '#8B4513', '#A52A2A', '#BC8F8F', '#DEB887', '#F4A460'],
  },
];

const color = ref('');
// 背景颜色设置
const setThisColor = () => {
  setColor(color.value);
};
// 背景颜色设置
function setColor(color) {
  const workspace = canvasEditor.canvas.getObjects().find((item) => item.id === 'workspace');
  workspace.set('fill', color);
  canvasEditor.canvas.renderAll();
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
:deep(.ivu-form-item) {
  margin-bottom: 0;
}
.img {
  width: 50px;
  padding: 5px;
  background: #f5f5f5;
  margin-left: 2px;
  height: 70px;
  cursor: pointer;
}

.color-list {
  padding: 10px 0;
  .item {
    padding-bottom: 5px;
  }
  span {
    display: inline-block;
    margin-left: 6px;
    background: #f5f5f5;
    height: 20px;
    width: 20px;
    font-size: 12px;
    line-height: 20px;
    vertical-align: middle;
    cursor: pointer;
  }
}

:deep(.ivu-divider-plain) {
  &.ivu-divider-with-text-left {
    margin: 10px 0;
    font-weight: bold;
  }
}
</style>
