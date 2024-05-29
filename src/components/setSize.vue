<template>
  <div v-if="!mixinState.mSelectMode">
    <Divider plain orientation="left">{{ $t('size') }}</Divider>
    <Form class="form-wrap">
      <FormItem prop="name" style="margin-right: 10px">
        <Input type="number" disabled v-model="width" @on-change="setSize">
          <template #prepend>
            <span>{{ $t('width') }}</span>
          </template>
        </Input>
      </FormItem>
      <FormItem prop="name">
        <Input type="number" disabled v-model="height" @on-change="setSize">
          <template #prepend>
            <span>{{ $t('height') }}</span>
          </template>
        </Input>
      </FormItem>
    </Form>
    <Button type="primary" @click="() => (showModal = true)">调整尺寸</Button>

    <Modal
      v-model="showModal"
      :title="$t('setSizeTip')"
      @on-ok="handleConfirm"
      @on-cancel="handleClose"
    >
      <p>{{ $t('default_size') }}</p>
      <ButtonGroup vertical style="margin: 10px 0">
        <Button
          v-for="(item, i) in presetSize"
          :key="`${i}presetSize`"
          size="default"
          style="text-align: left"
          @click="setSizeBy(item.width, item.height)"
        >
          {{ item.label }}:{{ item.width }}x{{ item.height }}
        </Button>
      </ButtonGroup>
      <Form class="form-wrap" style="justify-content: flex-start">
        <FormItem prop="name" style="margin-right: 10px">
          <Input type="number" v-model="modalData.width">
            <template #prepend>
              <span>{{ $t('width') }}</span>
            </template>
          </Input>
        </FormItem>
        <FormItem prop="name">
          <Input type="number" v-model="modalData.height">
            <template #prepend>
              <span>{{ $t('width') }}</span>
            </template>
          </Input>
        </FormItem>
      </Form>
    </Modal>
  </div>
</template>

<script setup name="CanvasSize">
import { Modal } from 'view-ui-plus';
import useSelect from '@/hooks/select';
import { useI18n } from 'vue-i18n';

const { mixinState, canvasEditor } = useSelect();
const { t } = useI18n();

const DefaultSize = {
  width: 1200,
  height: 900,
};

const showModal = ref(false);
const modalData = reactive({
  width: DefaultSize.width,
  height: DefaultSize.height,
});
let width = ref(DefaultSize.width);
let height = ref(DefaultSize.height);
let presetSize = reactive([
  {
    label: t('type_vertical'),
    width: 900,
    height: 1200,
  },
  {
    label: t('type_horizontal'),
    width: 1200,
    height: 900,
  },
  {
    label: t('phone_wallpaper'),
    width: 1080,
    height: 1920,
  },
  {
    label: 'kindle',
    width: 1200,
    height: 860,
  },
  {
    label: 'kindle-resize',
    width: 860,
    height: 1200,
  },
]);

onMounted(() => {
  canvasEditor.setSize(width.value, height.value);
  canvasEditor.on('sizeChange', (width, height) => {
    width.value = width;
    height.value = height;
  });
});

const setSizeBy = (w, h) => {
  modalData.width = w;
  modalData.height = h;
};
const setSize = () => {
  canvasEditor.setSize(width.value, height.value);
};

const handleClose = () => {
  showModal.value = false;
};

const handleConfirm = () => {
  width.value = modalData.width;
  height.value = modalData.height;
  setSize();
  handleClose();
};
</script>

<style scoped lang="less">
:deep(.ivu-form-item) {
  margin-bottom: 0;
}
:deep(.ivu-divider-plain) {
  &.ivu-divider-with-text-left {
    margin: 10px 0;
    font-weight: bold;
  }
}

.form-wrap {
  width: 250px;
  display: flex;
  justify-content: space-around;
  align-content: center;
  margin-bottom: 10px;
}
</style>
