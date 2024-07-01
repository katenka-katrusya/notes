<script setup>
import TagsList from '@/components/UI/TagsList.vue';

const props = defineProps({
  notes: {
    type: Array,
    required: true,
  }
});

const emits = defineEmits(['onRemove']);

const onRemove = (index) => {
  emits('onRemove', index);
};

const checkTags = (note) => {
  return note.tags && note.tags.length;
};

</script>

<template>
  <ul class="notes-list">
    <li class="note-item" v-for="(note, index) in notes" :key="index">
      <div class="note-header">
        <p>{{ note.title }}</p>
        <span class="note-remove" @click="onRemove(index)">&#10005;</span>
      </div>
      <div class="note-footer">
        <TagsList v-if="checkTags(note)"
                  :items="note.tags"
                  is-preview
        />
      </div>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
.notes-list {
  padding: 40px 0;
}

.note-item {
  width: 100%;
  padding: 18px 20px;
  margin-bottom: 20px;
  border-radius: 14px;
  background-color: #ffffff;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.02);

  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.04);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.note-remove {
  cursor: pointer;
}

.note-footer {
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: start;
}
</style>
