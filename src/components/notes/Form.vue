<script setup>
import { ref } from 'vue';
import TagsList from '@/components/UI/TagsList.vue';

const emits = defineEmits(['onSubmit']);

const value = ref('');
const selectedTags = ref([]);
const tags = ['дом', 'продукты', 'работа', 'отдых', 'прочее'];

const handleTagClick = (tag) => {
  if (!selectedTags.value.includes(tag)) {
    selectedTags.value.push(tag);
  } else {
    selectedTags.value = selectedTags.value.filter((t) => t !== tag);
  }
  console.log(selectedTags.value);
}

const onSubmit = () => {
  emits('onSubmit', value.value, selectedTags.value);
  value.value = '';
  selectedTags.value = [];
}
</script>

<template>
  <div class="note-form__wrapper">
    <form class="note-form" @submit.prevent="onSubmit">
      <textarea class="note-textarea" required
                v-model="value"
                placeholder="Type ur note"
      />
      <TagsList :items="tags" :activeTags="selectedTags" @onItemClick="handleTagClick" />
      <button class="btn btnPrimary" type="submit">Добавить заметку</button>
    </form>
  </div>
</template>

<style lang="scss" scoped>
.note-form__wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.note-form {
  display: flex;
  flex-direction: column;
  max-width: 600px;
  width: 100%;
}

.note-textarea {
  margin-bottom: 0;
}

.btn {
  margin-top: 10px;
  align-self: center;
}
</style>
