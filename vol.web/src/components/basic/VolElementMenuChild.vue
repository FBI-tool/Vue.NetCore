<template>
  <div class="vol-el-menu-item">
    <template v-for="item in list">
      <template v-if="item.children && item.children.length">
        <el-menu-item
          :key="item.id"
          :index="'' + item.id"
          v-if="!item.children.length && (!enable || item.enable == 1)"
        >
          <template #title></template>
          <span> {{ $ts(item.name) }}</span>
        </el-menu-item>
        <el-sub-menu
          :key="item.id"
          :index="'' + item.id"
          v-if="item.children.length && (!enable || item.enable == 1)"
        >
          <template #title>
            <span> {{ $ts(item.name) }}</span>
          </template>
          <vol-element-menu-child :enable="enable" :list="item.children" />
        </el-sub-menu>
      </template>
      <template v-else>
        <el-menu-item
          :key="item.id"
          :index="'' + item.id"
          v-if="!enable || item.enable == 1"
        >
          <template #title></template>
          <span> {{ $ts(item.name) }}</span>
        </el-menu-item>
      </template>
    </template>
  </div>
</template>

<script>
export default {
  name: "vol-element-menu-child",
  props: {
    list: {
      type: Array,
      default: [],
    },
    enable: {
      type: Boolean,
      default: false, //是否判断enable=1
    },
  },
};
</script>

<style scoped lang="less">
.vol-el-menu-item ::v-deep(.el-menu-item) {
  height: 42px !important;
  line-height: 42px !important;
}
i[class^='bi-'] {
  margin-right: 5px;
  width: var(--el-menu-icon-width);
  text-align: center;
  font-size: 16px;
  vertical-align: middle;
}
</style>
