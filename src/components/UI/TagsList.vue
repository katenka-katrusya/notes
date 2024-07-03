<script setup>
const props = defineProps({
  items: {
    type: Array,
    required: true,
  },
  activeTags: {
    type: Array,
    default: () => [],
  },
  isPreview: {
    type: Boolean,
    default: false,
  }
});

const emits = defineEmits(['onItemClick']);

const onItemClick = (item) => {
  emits('onItemClick', item);
};

const isActive = (item) => {
  return props.activeTags.includes(item);
}
</script>

<template>
  <ul class="tags-list">
    <li class="tag-item"
        v-for="item in items" :key="item"
        @click="onItemClick(item)"
        :class="{ isPreview: isPreview, isActive: isActive(item) }"
    >
      <span>{{ item }}</span>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
.tags-list {
  padding: 10px 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
}

.tag-item {
  padding: 8px 22px;
  background-color: #fff;
  border-radius: 22px;
  user-select: none;
  cursor: pointer;

  &.isActive {
    background-color: #444ce0;
    color: #fff;
  }

  &.isPreview {
    padding: 0;
    color: #444ce0;
    cursor: default;

    &:before {
      content: '#';
    }
  }
}
</style>
