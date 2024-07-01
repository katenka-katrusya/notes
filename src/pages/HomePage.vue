<script setup>
import Form from '@/components/notes/Form.vue';
import List from '@/components/notes/List.vue';
import { onMounted, reactive, watch } from 'vue';

const notes = reactive([]);

const handlerSubmit = (title, selectedTags) => {
  const note = {
    title,
    tags: selectedTags,
  };
  notes.push(note);
  console.log(note);
};

const handlerRemove = (index) => {
  notes.splice(index, 1);
};

const getInitialNotes = () => {
  const localNotes = localStorage.getItem('notes');
  return localNotes ? JSON.parse(localNotes) : [];
}

onMounted(() => {
  notes.push(...getInitialNotes());
});

watch(() => notes, (updNotes) => {
      localStorage.setItem('notes', JSON.stringify(updNotes));
    },
    { deep: true }
);
</script>

<template>
  <Form @onSubmit="handlerSubmit"/>
  <List @onRemove="handlerRemove" :notes="notes"/>
</template>

<style scoped>

</style>
